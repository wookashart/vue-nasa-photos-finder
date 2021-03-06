<template>
  <div :class="[{ flexStart: step === 1}, 'home']">
    <transition name="slide">
      <div class="logo" v-if="step === 1">
        <p>NASA PHOTOGRAPHY FINDER</p>
      </div>
    </transition>
    <Claim v-if="step === 0" />
    <Search v-model="searchValue" @input="handleInput" />
    <div class="results" v-if="results && !loading && step === 1">
      <Item v-for="(item, index) in results" :item="item" :key="index" @click.native="handleModalOpen(item)" />
    </div>
    <div class="loader" v-if="step === 1 && loading" />
    <Modal v-if="modalOpen" @closeModal="modalOpen = false" :item="modalItem" />
  </div>
</template>

<script>
  import axios from 'axios';
  import debounce from 'lodash.debounce';
  import Claim from '@/components/Claim';
  import Search from '@/components/Search';
  import Item from '@/components/Item'
  import Modal from '@/components/Modal'

  const API = 'https://images-api.nasa.gov/search';

  export default {
    name: 'home',
    data() {
      return {
        searchValue: '',
        results: [],
        loading: false,
        step: 0,
        modalOpen: false,
        modalItem: null,
      }
    },
    components: {
      Claim,
      Search,
      Item,
      Modal,
    },
    methods: {
      handleModalOpen(item) {
        this.modalOpen = true;
        this.modalItem = item;
      },
      handleInput: debounce(function() {
        this.loading = true;

        axios.get(`${API}?q=${this.searchValue}&media_type=image`)
          .then(response => {
            console.log(response);

            this.results = response.data.collection.items;
            this.loading = false;
            this.step = 1;
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

    &.flexStart {
      justify-content: flex-start;
    }

    .logo {
      position: absolute;
      top: 0;
      left: 50px;

      p {
        font-weight: 700;
      }
    }

    .slide-enter-active,
    .slide-leave-active {
      transition: margin-top 0.3s ease;
    }

    .slide-enter,
    .slide-leave-to {
      margin-top: -50px;
    }

    .results {
      margin-top: 50px;
      display: grid;
      grid-template-columns: 1fr;
      grid-gap: 20px;

      @media (min-width: 768px) {
        grid-template-columns: 1fr 1fr;
      }

      @media (min-width: 1024px) {
        grid-template-columns: 1fr 1fr 1fr;
      }
    }

    .loader {
      margin-top: 100px;
      display: inline-block;
      width: 64px;
      height: 64px;

      @media (min-width: 768px) {
        width: 90px;
        height: 90px;
      }
    }

    .loader:after {
      content: " ";
      display: block;
      width: 46px;
      height: 46px;
      margin: 1px;
      border-radius: 50%;
      border: 5px solid black;
      border-color: black transparent black transparent;
      animation: lds-dual-ring 1.2s linear infinite;
    }
    
    @keyframes lds-dual-ring {
      0% {
        transform: rotate(0deg);
      }
      100% {
        transform: rotate(360deg);
      }
    }
  }
</style>