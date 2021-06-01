<template>
  <div id="app">
    <pagination-control :settings="settings">
    <PaginationControlSettings/>
    </pagination-control>
  </div>
</template>

<script>
import { PaginationControl } from 'vue-smart-pagination'

export default {
  name: 'App',
  components: {
    PaginationControl
  },
  data: function () {
    return {
      arrayData: [
        {
          data: 'Page № 1'
        },
        {
          data: 'Page № 2'
        },
        {
          data: 'Page № 3'
        },
        {
          data: 'Page № 4'
        },
        {
          data: 'Page № 5'
        },
        {
          data: 'Page № 6'
        },
        {
          data: 'Page № 7'
        },
        {
          data: 'Page № 8'
        },
        {
          data: 'Page № 9'
        },
        {
          data: 'Page № 10'
        },
        {
          data: 'Page № 11'
        },
        {
          data: 'Page № 12'
        },
      ]
    }
  },
  computed: {
    settings: function () {
      return {
        arrayData: this.arrayData
      }
    }
  }
}
</script>
