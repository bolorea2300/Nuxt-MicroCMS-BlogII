<template>
  <div>
    <div class="header">
      <div class="size">
        <div id="title"><nuxt-link to="/">Pincer's Blog</nuxt-link></div>

        <ul>
          <li><nuxt-link to="/admin">管理人について</nuxt-link></li>
          <li><nuxt-link to="/policy">プライバシーポリシー</nuxt-link></li>
          <li><nuxt-link to="/contact">お問い合わせ</nuxt-link></li>
        </ul>
      </div>
    </div>

    <div class="clear"></div>
    <div class="main">
      <nuxt />
    </div>
  </div>
</template>

<style>
.header {
  width: 100%;
}

.size {
  width: 98%;
  max-width: 1100px;
  margin: 0 auto;
}

#title {
  text-align: center;
  font-size: 32px;
}

#title a {
  text-decoration: none;
  color: black;
}

.header ul {
  padding: 0;
}

.header ul li {
  list-style: none;
  float: left;
  width: 33%;
  text-align: center;
}

.header ul li a {
  display: block;
  text-decoration: none;
  color: black;
  transition: 0.2s;
  font-size: 16px;
}

.header ul li a:hover {
  font-size: 12px;
}

.header ul li + li {
  border-left: 1px solid black;
}

@media screen and (min-width: 769px) {
}

@media screen and (max-width: 768px) {
}

.main {
  width: 98%;
  max-width: 1100px;
  margin: 0 auto;
  margin-top: 50px;
  padding: 10px;
}
</style>
