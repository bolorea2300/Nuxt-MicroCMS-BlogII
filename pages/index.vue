<template>
  <div class="width">
    <div class="articles">
      <div
        class="article"
        v-for="list in data.contents"
        :key="data.contents.id"
      >
        <div class="image">
          <img :src="list.image.url" alt="画像" />
          <nuxt-link :to="'/article/' + list.id"></nuxt-link>
        </div>

        <div class="frame">
          <h3 class="titlelink">
            <nuxt-link :to="'/article/' + list.id">{{ list.title }}</nuxt-link>
          </h3>

          <div class="tags">
            <div class="tag" v-for="(data, id) in list.tags" :key="id">
              <nuxt-link
                v-text="data.tagname"
                :to="'/tag/' + data.id"
              ></nuxt-link>
            </div>
          </div>
          <div class="clear"></div>
        </div>
      </div>
    </div>

    <div class="page">
      <p>
        <nuxt-link v-if="number > 1" :to="'?page=' + (number - 1)"
          >Prev</nuxt-link
        >
        <nuxt-link :to="'?page=' + (number + 1)">Next</nuxt-link>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "index",
  watchQuery: ["page"],
  head() {
    return {
      titleTemplate: null,
      meta: [
        {
          hid: "description",
          property: "description",
          content: "Pincerという者が運営するブログです。",
        },
      ],
    };
  },
  data() {
    return {
      page: 1,
    };
  },
  async asyncData({ $microcms, route, error }) {
    let number;

    if (route.query.page) {
      number = route.query.page;
    } else {
      number = 1;
    }

    try {
      const data = await $microcms.get({
        endpoint: "article",
        queries: {
          limit: 12,
          orders: "-createdAt",
          offset: (number - 1) * 12,
          fields: "id,title,image,tags,createdAt",
        },
      });

      return { data: data };
    } catch (err) {
      error({
        statusCode: 404,
        reason: "ページ一覧が取得できません",
        message: "しばらくしてからお試しください。",
      });
    }
  },
  computed: {
    number: function () {
      if (this.$route.query.page) {
        return parseInt(this.$route.query.page);
      } else {
        return 1;
      }
    },
  },
  watch: {
    page(from) {
      this.$router.push("?page=" + from);
    },
  },
};
</script>

<style>
.articles {
  display: grid;
}

.article {
  border: 1px solid black;
  border-radius: 10px;
  overflow: hidden;
  position: relative;
  margin: 10px;
  box-shadow: 2px 2px 2px 2px rgba(0, 0, 0, 0.5);
}

.frame {
  padding: 10px;
}

@media screen and (min-width: 561px) {
  .articles {
    grid-template-columns: 1fr 1fr;
  }
}

@media screen and (min-width: 961px) {
  .articles {
    grid-template-columns: 1fr 1fr 1fr;
  }
}

@media screen and (max-width: 560px) {
}

.image {
  position: relative;
  height: 300px;
  overflow: hidden;
}

.image a {
  position: absolute;
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
  transition: 0.2s;
}

.image a:hover {
  background-color: rgba(0, 255, 0, 0.5);
}

.page p {
  text-align: center;
}

.article img {
  height: 100%;
  width: 100%;
  object-fit: cover;
}

.article .titlelink a {
  text-decoration: none;
  transition: 0.2s;
  color: black;
}

.article .titlelink a:hover {
  color: red;
}
</style>
