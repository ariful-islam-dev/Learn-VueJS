<script>
  import DemoGrid from './components/GridComponent.vue'
  export default {
    components: {
      DemoGrid
    },
    data: ()=>({
      searchQuery: '',
      gridColumns: ['name', 'power'],
      gridData: [
        {name: 'Chuck Norris', power: Infinity},
        {name: 'Bruce Lee', power: 9000},
        {name: 'Jackie Chan', power: 7000},
        {name: 'Jet Li', power: 8000}
      ]
    })
  }
</script>
<template>
  <form id="search">
    Search <input type="text" name="query" v-model="searchQuery">
  </form>
  <DemoGrid
    :data="gridData"
    :columns="gridColumns"
    :filter-key="searchQuery"
  />
</template>
<style>
#search{
  font-size: 20px;
  color: #42b983;
  font-weight: bold;
  width: 90%;
  margin:  0 auto;
}
input{
  border: 2px solid #42b983;
  width: 100%;
  display: inline-block;
  padding: 5px;
  font-size: 20px;
  border-radius: 10px;
}
</style>