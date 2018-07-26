<template>
  <div id="app">
    <search-bar v-on:changekeyword=sendkeyword></search-bar>
    <naver-list v-bind:tophun="tophun" ></naver-list>

  </div>
</template>

<script>
  import HelloWorld from './components/HelloWorld'
  import cleanStr from './add_js/cleanString'
  import NaverList from './components/NaverList'
  import SearchBar from './components/SearchBar'
  import axios from 'axios'

  let clientId = "K99rkGyg42Jf0FBSTQgO";
  let clientSecret = "M0BbIqUL5F";


  export default {
    name: 'App',
    comments: {
      NaverList,
    },
    data() {
      return {
        title: [],
        link: [],
        tophun: [],
        parentKeyWord: "세종대"
      }
    },
    mounted() {
      this.search();
    },
    methods: {
      search: function () {
        axios({
          method: "get",
          url: "/naversearch",
          params: {
            query: this.parentKeyWord,
            display: "100"
          },
          crossDomain: true,
          headers: {
            "X-Naver-Client-Id": clientId,
            "X-Naver-Client-Secret": clientSecret
          }
        }).then((result) => {
          //console.log(result.data.items[50]);
          let news = result.data.items;
          for (let i in news) {
            var tmp = {
              title: cleanStr(news[i].title, "title"),
              link: (news[i].originallink)
            };
            this.tophun.push(tmp);
          }
        })
      },
      sendkeyword:function (val) {
        this.tophun=[];
        this.parentKeyWord = val;
        this.search();
      }
    },
    components: {
      NaverList,
      HelloWorld,
      SearchBar
    }
  }
</script>

<style>
  #app {
    margin: 10px auto;
    width: 1000px;
  }
</style>
