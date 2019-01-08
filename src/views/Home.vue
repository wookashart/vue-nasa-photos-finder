<template>
  <div class="home">
    <Claim />
    <search />
  </div>
</template>

<script>
  import axios from 'axios';
  import debounce from 'lodash.debounce';
  import Claim from '../components/Claim';
  import Search from '../components/Search';

  const API = 'https://images-api.nasa.gov/search';

  export default {
    name: 'home',
    data() {
      return {
        searchValue: '',
        results: [],
      }
    },
    components: {
      Claim,
      Search,
    },
    methods: {
      handleInput: debounce(function() {
        axios.get(`${API}?q=${this.searchValue}&media_type=image`)
          .then(response => {
            this.results = response.data.collection.items;
          })
          .catch(err => {
            console.log(err);
          })
      }, 500)
    },
  };
</script>


<style lang="scss" scoped>
  .home {
    display: flex;
    flex-flow: column;
    align-items: center;
    justify-content: center;
    margin: 0;
    padding: 30px;
    width: 100%;
    box-sizing: border-box;
    height: 100vh;
  }
</style>