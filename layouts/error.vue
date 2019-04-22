<template>
  <v-content>
    <v-container
      light
      text-xs-center
      style="font-family: 'Ubuntu mono'"
    >
      <h1 v-if="error.statusCode === 404">404, Page does not exist...</h1>
      <h1 v-else>Something wrong on this application... so sad.</h1>
      <br>
      <br>
      <nuxt-link to="/">Home</nuxt-link>
    </v-container>
  </v-content>
</template>

<script>
export default {
  props: {
    error: {
      default: () => [],
      type: Object
    }
  },
  layout: "blog"
};
</script>
