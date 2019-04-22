<template>
  <v-app>
    <v-toolbar
      fixed
      flat
      app
      color="white"
      style="font-family: 'Courier New', monospace;"
    >
      <v-spacer />
      <v-btn
        icon
        href="https://yuantian1991.github.io/"
      >
        <v-avatar
          :size="40"
          color="white lighten-4"
        >
          <img
            src="~/assets/image/QQ.jpg"
            alt="avatar"
          >
        </v-avatar>
      </v-btn>
      <v-toolbar-title class="hidden-sm-and-down">
        <a
          id="title"
          href="https://yuantian1991.github.io/"
          style="color: black;"
        > {{ title }} </a>
      </v-toolbar-title>

      <v-spacer />
      <v-menu offset-y>
        <v-btn
          slot="activator"
          flat
        >Life/生活</v-btn>
        <v-list>
          <v-list-tile
            v-for="(item, index) in WordsLink"
            :key="index"
            :href="item.link"
          >
            <v-list-tile-title
              class="body-1"
              style="font-family: 'Courier New', monospace;"
            >{{ item.title }}</v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-menu>
      <v-spacer />
    </v-toolbar>

    <nuxt />

    <Footer />
  </v-app>
</template>

<script>
import Footer from "~/components/Footer";
export default {
  components: {
    Footer: Footer
  },
  data() {
    return {
      fixed: true,
      items: [
        { icon: "apps", title: "Welcome", to: "/" },
        { icon: "bubble_chart", title: "Inspire", to: "/inspire" }
      ],
      title: "Yuan Tian",
      WordsLink: [
        { title: "Think/随感", link: "https://yuantian-think.postach.io/" },
        { title: "Articles/长文", link: "https://yuantian.postach.io/" },
        {
          title: "500px/摄影",
          link: "https://500px.com/tianyuan1991hit"
        },
        { title: "TMDB/电影", link: "https://www.themoviedb.org/list/96648" },
        { title: "Cook/菜谱", link: "https://yuan-cookbook.postach.io/" }
      ]
    };
  }
};
</script>

<style>
#title {
  text-decoration: none;
}
#title:hover {
  font-weight: bolder;
}
</style>