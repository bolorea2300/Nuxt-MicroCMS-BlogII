<template>
  <div class="contact">
    <h1>お問い合わせ</h1>

    <ul>
      <li>
        Twitter:<a href="https://twitter.com/logo8505" target="_Blank"
          >@logo8505</a
        >
      </li>
    </ul>

    <iframe
      src="https://docs.google.com/forms/d/e/1FAIpQLSeqJjqMyYFoxkl6hPX3mrmLkD3Tp8ryGjaKmyZXTkAE6HxAyA/viewform?embedded=true"
      width="640"
      height="574"
      frameborder="0"
      marginheight="0"
      marginwidth="0"
      >読み込んでいます…</iframe
    >
  </div>
</template>

<script>
export default {
  name: "Contact",
  head() {
    return {
      title: "お問い合わせ",
      meta: [{ hid: "robots", name: "robots", content: "noindex" }],
    };
  },
};
</script>
