<template>
  <div class="outerWrapper">
    <div class="innerWrapper">
      <div class="photo">
        <img :src="this.photo" />
      </div>
      <div class="description">
        <h2>{{ this.title }}</h2>
        <p class="description">{{ this.description }}</p>
      </div>
    </div>
    <div class="close" @click="$emit('closeModal')" />
  </div>
</template>

<script>
export default {
  name: 'Modal',
  data() {
    return {
      photo: null,
      title: null,
    };
  },
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
    this.description = this.item.data[0].description;
  }
}
</script>

<style lang="scss" scoped>
  .outerWrapper {
    background-color: #f6f6f6;
    max-width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;

    @media (min-width: 1024px) {
      max-width: 70%;
      height: 60%;
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      margin: auto;
      box-shadow: 0 30px 30px -10px rgba(0,0,0, 0.3)
    }
  }

  .close {
    position: absolute;
    right: 0;
    top: 0;
    width: 30px;
    height: 30px;
    padding: 30px;
    cursor: pointer;

    &::before,
    &::after {
      content: '';
      position: absolute;
      width: 20px;
      height: 2px;
      background-color: black;
      display: block;
      top: 30px;
      right: 20px;
    }

    &::before {
      transform: rotate(45deg);
    }

    &::after {
      transform: rotate(-45deg);
    }
  }

  .innerWrapper {
    display: flex;
    height: 100%;
    padding: 50px;
    justify-content: center;
    align-items: center;
    flex-flow: column;

    @media (min-width: 1024px) {
      flex-flow: row;

      .photo {
        width: 50%;
        margin-right: 20px;
      }
    }

    .photo {
      max-width: 500px;
      height: auto;
      background-color: black;

      img {
        max-width: 100%;
      }
    }

    .description {
      color: #333;
    }
  }
</style>
