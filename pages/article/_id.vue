<template>
  <div>
    <h1>{{ data.title }}</h1>

    <ul>
      <li>CREATE:{{ time(data.createdAt) }}</li>
      <li>UPDATE:{{ time(data.updatedAt) }}</li>
    </ul>

    <a
      href="https://twitter.com/share?ref_src=twsrc%5Etfw"
      class="twitter-share-button"
      data-show-count="false"
      >Tweet</a
    >

    <div class="tags">
      <div class="tag" v-for="(data, id) in data.tags" :key="id">
        <nuxt-link v-text="data.tagname" :to="'/tag/' + data.id"></nuxt-link>
      </div>
    </div>

    <div class="clear"></div>

    <div class="content mt-50" v-html="data.body"></div>
  </div>
</template>

<script>
import dayjs from "dayjs";
import utc from "dayjs/plugin/utc";
import timezone from "dayjs/plugin/timezone";

dayjs.extend(utc);
dayjs.extend(timezone);

export default {
  name: "article",
  head() {
    return {
      title: this.data.title,
      meta: [
        {
          hid: "description",
          property: "description",
          content: this.data.description,
        },
        {
          hid: "og:description",
          property: "og:description",
          content: this.data.description,
        },
        {
          hid: "og:url",
          property: "og:url",
          content: this.$route.params.id,
        },
        { hid: "og:image", property: "og:image", content: this.data.image.url },
      ],
      script: [
        {
          src: "https://platform.twitter.com/widgets.js",
        },
      ],
    };
  },
  async asyncData({ $microcms, route, redirect }) {
    const data = await $microcms
      .get({
        endpoint: "article",
        contentId: route.params.id,
        queries: {
          fields: "id,title,description,image,tags,body,createdAt,updatedAt",
        },
      })
      .catch((res) => redirect("/404"));
    return { data: data };
  },
  methods: {
    time: function (data) {
      return dayjs.utc(data).tz("Asia/Tokyo").format("YYYY-MM-DD");
    },
  },
};
</script>
