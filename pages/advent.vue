<template>
  <v-data-table
    :headers="headers"
    :items="advents"
    :items-per-page="5"
    class="elevation-1"
  >
    <template v-slot:item.starCount="{ item }">
      <v-icon color="yellow" v-for="i in item.starCount">star</v-icon>
    </template>
    <template v-slot:item.url="{ item }">
      <a :href="item.url" target="_blank" class="pa-2 text--no-underline">
        <v-icon height="30" width="30">open_in_new</v-icon>
      </a>
    </template>
  </v-data-table>
</template>

<script>
import {advents} from '@/data/adventInfo.js';
export default {
  name: 'advent',
  data () {
    return {
      headers: [
        {
          text: 'Challenge Day',
          align: 'start',
          sortable: true,
          value: 'day',
        },
        {
          text: 'Stars',
          align: 'start',
          sortable: true,
          value: 'starCount',
        },
        {
          text: 'Solution',
          align: 'start',
          sortable: true,
          value: 'url',
        },
        {
          text: 'Tools Used',
          align: 'start',
          sortable: true,
          value: 'tools',
        },
      ],
      advents
    }
  },
}
</script>

<style lang="scss" scoped>
  .text--no-underline {
    text-decoration: none;
  }
</style>
