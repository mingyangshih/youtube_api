<template>
  <div class="home">
    <!-- <img :src="item.snippet.thumbnails.default.url" alt="" v-for="(item, idx) in videoary" :key="idx"> -->
    <!-- <div class="iframe" v-for="(item,idx) in videoary" :key="idx" v-html="item.player.embedHtml"> -->
    <!-- </div> -->
  </div>
</template>

<script>


export default {
  data() {
    return {
      videoary: [],
    };
  },
  name: 'Home',
  components: {
  },
  created() {
    // set fetch 要送出的資料因為GET不能直接帶參數
    const url = new URL(`${process.env.VUE_APP_VIDEOS_LIST}`);
    url.search = new URLSearchParams({
      part: 'snippet,contentDetails,statistics,localizations,player',
      chart: 'mostpopular',
      maxResults: 20,
      h1: 'zh-TW',
      maxHeight: 72,
      maxWidth: 100,
      key: `${process.env.VUE_APP_KEY}`,
    });
    // run fetch
    fetch(url).then((response) => response.json()).then((myJson) => {
      console.log(myJson);
      this.videoary = myJson.items;
    });
  },
};
</script>
