<template>
    <section class="search-box">
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Search..."
          v-model="query"
          @keypress.enter="search"
          />
      </section>
</template>

<script>

export default {
    props: ['v-model', 'onSearch'],
    name: 'SearchBar',
    data () {
        return {
        query: '',
         }
    },
    methods: {
        search () {
                this.onSearch({
                    query: this.query,
                    })
                console.log(this.query)
            
        }
    }
}


</script>
