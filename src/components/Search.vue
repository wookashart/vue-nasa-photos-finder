<template>
  <div class="searchWrapper">
    <input
      type="text"
      name="search"
      id="search"
      placeholder="ex. Moon"
      :value="value"
      @input="handleChange"
    />
  </div>
</template>

<script>
export default {
  name: 'Search',
  props: {
    value: {
      type: String,
      required: true,
    }
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  }
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
      font-size: 18px;
      font-weight: 700;
    }
  }
</style>