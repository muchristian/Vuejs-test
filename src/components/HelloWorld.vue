<template>
  <nav class="pagination">
                      <a v-on:click="prev()" class="button">Previous</a>
                      <a v-on:click="next()" class="button">Next page</a>
                      <ul>
                        <li v-for="p in pageCount" :key="p">
                          <a v-if="pageNo == p" v-on:click="page(p)" class="button is-primary">{{p}}</a>
                          <a v-else v-on:click="page(p)" class="button">{{p}}</a>
                        </li>
                      </ul>
                    </nav>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
