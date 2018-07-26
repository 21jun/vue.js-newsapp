<template>
  <v-layout row wrap align-center>
    <link href='https://fonts.googleapis.com/css?family=Roboto:300,400,500,700|Material+Icons' rel="stylesheet">
    <link href="https://cdn.jsdelivr.net/npm/vuetify/dist/vuetify.min.css" rel="stylesheet">
    <v-flex v-for=" item in tophun">
      <v-card width="900px" height="40px" style="line-height: 10px;">
        <a v-bind:href="item.link" style="text-decoration: none; color: black;">
          <v-card-text>{{item.title}}</v-card-text>
        </a>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
  export default {
    name: "NaverList",
    props: ["tophun", "links"],
    methods: {
      linking: function (link) {
        window.open(link);
      }
    }
  }
</script>

<style scoped>

</style>
