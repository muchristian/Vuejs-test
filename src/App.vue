
<template>

  <div id="app">
  <ul v-for="(u, idx) in users" :key="idx">
                  <td>{{u.id}}</td>
                </ul>
  <nav aria-label="Page navigation example">
  <ul class="pagination">
    <li class="page-item"><a v-on:click="prev()" class="page-link">Previous</a></li>
    <li v-for="(p, idx) in pageCount" :key="idx">
                          <a v-if="pageNo == p" v-on:click="page(p)" class="page-link active">{{p}}</a>
                          <a v-else v-on:click="page(p)" class="page-link">{{p}}</a>
                        </li>
    <li class="page-item"><a v-on:click="next()" class="page-link">Next page</a></li>
  </ul>
</nav>
  </div>
</template>

<script>
import "./assets/css/bootstrap.min.css"
export default {
  name: 'App',
data: function() {
  return {
    users: [],
    pageNo: 1,
    pageSize: 10,
    pageCount: 0
  }
    
  },
  methods: {
    init: function(){ 
      this.virtualService({
        pageNo: this.pageNo,
        pageSize: this.pageSize
      });
    },
    page: function(pageNo) { 
     
     this.virtualService({
        pageNo: pageNo,
        pageSize: this.pageSize
      });
    },
    first: function() {
        this.pageNo = 1; 
        this.virtualService({
          pageNo:this.pageNo,
          pageSize:this.pageSize
        });
    },
    next: function() {
      if(this.pageNo < this.pageCount) {
        this.pageNo += 1;
        this.virtualService({
          pageNo:this.pageNo,
          pageSize:this.pageSize
        });
      }
    },
    virtualDataFromDb: function() {
      var users = [];
      for(var i = 1; i <= 105; i++){
        var user = {
          id: "RW"+i,
        };
        users.push(user);
      }
      return users;
    },
    count: function(){
      return this.virtualDataFromDb().length;
    },
    queryFromVirtualDB: function(condition, startRow, endRow){
      var result = [];
      var data = this.virtualDataFromDb();
      var count = this.count(condition);
      for(var i = startRow - 1; i < endRow; i++) {
        if(i < count){
          result.push(data[i]);
        }
      }
      return result;
    },
    virtualService: function(params){
      
      var condition = {};
      var pageNo = params.pageNo;
      var pageSize = params.pageSize;
      var pageCount = Math.ceil(this.count(condition) / pageSize);
				
      if (pageNo == 0) pageNo = 1;
      if (pageNo < 0) pageNo = pageCount;
      else if (pageNo > pageCount) pageNo = pageCount;
      var startRow = (pageNo - 1) * pageSize + 1; 
      var endRow = startRow + pageSize - 1;
      var data = this.queryFromVirtualDB(condition, startRow, endRow);
      
      this.users = data;
      this.pageNo = pageNo;
      this.pageCount = pageCount;
      
    }
  },
  created: function(){
    // this.init();
  },
  // ready
  mounted: function(){
    this.init();
  }
}
</script>
<style>
.active {
  background: dodgerblue;
  color: white !important;
}
.page-link:hover {
  background: dodgerblue !important;
  color: white !important;
}
</style>
