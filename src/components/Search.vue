<template>
  <div class="searchWrapper">
    <input type="text" name="search" id="search" v-model="searchValue" @input="handleInput" placeholder="ex. Moon" />
    <ul>
      <li v-for="item in results" :key="item.data[0].nasa_id">
        <p>{{ item.data[0].description }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Search',
}
</script>

<style lang="scss" scoped>
  .searchWrapper {
    width: 300px;
    display: flex;
    flex-flow: column;
    margin-top: 60px;

    input {
      height: 30px;
      border: 0;
      border-bottom: 1px solid black;
      outline: none;
      text-align: center;
    }
  }
</style>