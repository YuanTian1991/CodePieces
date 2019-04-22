<template>
  <v-content style="font-family: 'Cambria', mono;background-color:white">
    <v-container
      justify-center
      fill-height
    >

      <v-layout
        row
        wrap
        justify-center
        align-center
      >
        <v-flex
          xs12
          justify-center
        >
          <v-card-actions
            class="justify-center font-weight-black"
            style="padding:20px"
          >
            <v-card-title style="font-size:48px">Yuan Tian's Code Pieces</v-card-title>
          </v-card-actions>
          <v-divider />
        </v-flex>
        <v-flex
          v-for="(item,index) in codepieces"
          :key="index"
          xs12
          md4
          style="margin:1em"
        >
          <nuxt-link
            v-if="item.linktype === 'nuxt'"
            :to="item.link"
          >
            <v-card
              class="white elevation-5"
              height="200"
            >
              <v-card-title
                style="font-size:25px"
                class="font-weight-black grey darken-4 white--text"
              >
                {{ item.name }}
              </v-card-title>
              <v-card-title style="text-align:justify;font-size:15px">
                {{ item.des }}
              </v-card-title>

            </v-card>
          </nuxt-link>
          <a
            v-else
            :href="item.link"
          >
            <v-card
              class="white elevation-5"
              height="200"
            >
              <v-card-title
                style="font-size:25px"
                class="font-weight-black grey darken-4 white--text"
              >
                {{ item.name }}
              </v-card-title>
              <v-card-title style="text-align:justify;font-size:15px">
                {{ item.des }}
              </v-card-title>

            </v-card>
          </a>
        </v-flex>
      </v-layout>
    </v-container>
  </v-content>
</template>

<script>
export default {
  data() {
    return {
      codepieces: [
        {
          name: "Crossfilter On Nuxt.js",
          linktype: "a",
          link: "https://yuantian1991.github.io/Crossfilter_Nuxt_Example/",
          des:
            "When I was learning to use Crossfilter, I created something fancy on my GCGR project, which could generate a nice table, pie, and hist plot via a simple csv file."
        },
        {
          name: "Element-UI On Nuxt.js",
          linktype: "nuxt",
          link: "/cellfilter",
          des:
            "In my GCGR Project, I need to create a table for hosting all cell lines. Thus I firstly tried Element-UI, and it works well."
        }
      ]
    };
  }
};
</script>
