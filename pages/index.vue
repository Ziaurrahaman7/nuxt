<template>
  <div>
     <div class="container">
      <div class="row">
        <div class="col-12 text-center">
          <h1>All Blog</h1>
        </div>
          <div class="col-12">
            
              <div>
                  <b-col lg="6" class="my-1">
                      <b-form-group
                      label="Filter"
                      label-for="filter-input"
                      label-cols-sm="3"
                      label-size="sm"
                      class="mb-0"
                      >
                      <b-input-group size="sm">
                          <b-form-input
                          id="filter-input"
                          v-model="filter"
                          type="search"
                          height="40px"
                          placeholder="Type to Search"
                          ></b-form-input>

                          <b-input-group-append>
                          <b-button :disabled="!filter" @click="filter = ''">Clear</b-button>
                          </b-input-group-append>
                      </b-input-group>
                      </b-form-group>
                  </b-col>
              </div>
              <b-table
                  id="my-table"
                  :items="items"
                  :filter="filter"
                  :filter-included-fields="filterOn"
                  :per-page="perPage"
                  :current-page="currentPage"
                  small
                  @filtered="onFiltered"
                  ></b-table>
                  <b-pagination
                  v-model="currentPage"
                  :total-rows="rows"
                  :per-page="perPage"
                  aria-controls="my-table"
              ></b-pagination>
          </div>
      </div>
     </div>


     <!-- <vs-pagination :total-pages="20" @change="changePage"></vs-pagination> -->
  </div>
</template>
<script>
export default {
//    name:blogs,
 data() {
  return {
      search: '',
      perPage: 10,
      currentPage: 1,
      filter: null,
      filterOn: [],
      totalRows: 1,
      items:[], 
  }
 },
 async created() {
      const blogs = await this.$axios.$get('https://jsonplaceholder.typicode.com/posts')
     this.items= blogs
     console.log(this.items)
 },
 methods:{
  onFiltered(filteredItems) {
      // Trigger pagination to update the number of buttons/pages due to filtering
      this.totalRows = filteredItems.length
      this.currentPage = 1
    }
 },
 computed: {
    rows() {
      return this.items.length
    },
  }
}
</script>
<style>

</style>