<template>
  <v-content style="font-family: 'Cambria', mono;background-color:white">
    <v-container justify-center>
      <v-layout row>
        <v-flex
          xs12
          md8
          offset-md2
        >
          <v-layout
            row
            wrap
          >
            <v-flex
              v-for="(item,index) in celllines"
              :key="index"
              xs12
              md6
            >
              <nuxt-link
                :to="item.link"
                style="text-decoration:none"
              >
                <v-card
                  class="clickable"
                  height="15em"
                  :style="'margin:1em;background-color:' + item.color"
                >
                  <v-container
                    justify-center
                    fill-height
                  >
                    <v-card-title
                      class="font-weight-black white--text"
                      style="font-size:30px"
                    >
                      {{ item.title }}
                    </v-card-title>
                  </v-container>
                </v-card>
              </nuxt-link>
            </v-flex>
          </v-layout>
        </v-flex>
      </v-layout>
    </v-container>
  </v-content>
</template>

<script>
export default {
  // middleware: "admin",
  data() {
    return {
      celllines: [
        {
          title: "GNS cell lines unmodified",
          link: "/cellfilter/GNS_cell_lines_unmodified",
          color: "#D81B60"
        },
        {
          title: "GNS cell lines derivatives",
          link: "/cellfilter/GNS_cell_lines_derivatives",
          color: "#D81B60"
        },
        {
          title: "NS cell lines unmodified",
          link: "/cellfilter/NS_cell_lines_unmodified",
          color: "#3949AB"
        },
        {
          title: "NS cell lines derivatives",
          link: "/cellfilter/NS_cell_lines_derivatives",
          color: "#3949AB"
        }
      ]
    };
  }
};
</script>

<style>
clickable {
  cursor: pointer;
}
.clickable:hover {
  /* background-color: #dd3497; */
  color: white;

  background-image: linear-gradient(to bottom right, #0099ff, #0099ff);
}
</style>
