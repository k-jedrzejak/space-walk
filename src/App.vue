<template>
  <div class="page-container">

    

    <Transition name="slide">
      <LogoImage  v-if="step === 1"/>
    </Transition>

    <Transition name="fade">
      <HeroImage v-if="step === 0"/>
    </Transition>

    <div :class="[{flexStart: step ===1}, 'page-wrapper']">

      <ModalElement v-if="modalOpen" @closeModal="modalOpen = false" :item="modalData" />
      <div :class="[{narrow: step==0},'content']">

    
    
        <HeroClaim
          :title="title"
          :sentence="mainClaim"
          :subsentence="subClaim"
          v-if="step === 0"
        />
  
        <InputSearch 
          v-model="searchValue" 
          @input="getValue"
          :dark="step === 1"
          :class="{gap: step===1}"
        />

        <LoaderElement v-if="step === 1 && loading"/>

        <div class="images-container" v-if="results && !loading && step ===1">
          <SearchResults
            v-for="(item, i) in results"
            :key="i"
            :item="item"
            @click="handleModalOpen(item)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script> 
import InputSearch from "./components/InputSearch.vue";
import SearchResults from "./components/SearchResults.vue";
import HeroClaim from "./components/HeroClaim.vue"
import HeroImage from "./components/HeroImage.vue";
import LogoImage from "./components/LogoImage.vue";
import ModalElement from "./components/ModalElement.vue";
import LoaderElement from "./components/LoaderElement.vue";

import axios from "axios";
import debounce from "lodash.debounce"

const api = 'https://images-api.nasa.gov/search'

export default {
  name: 'App',
  components: {
    InputSearch,
    SearchResults,
    HeroClaim,
    HeroImage,
    LogoImage,
    ModalElement,
    LoaderElement,
    
},
  data() {
    return{
      searchValue: '',
      results: [],
      title: 'Space•Walk', 
      mainClaim: 'Begin your journey through our amazing galaxy, and discover places you never even heard of',
      subClaim: 'Type anything space-related to start',
      loading: false,
      step: 0,
      modalOpen: false,
      modalData: null
    }
  },
  methods: {
    getValue: debounce(function(){
      this.loading = true;
      axios.get(`${api}?q=${this.searchValue}&media_type=image`)
      .then((res) => {
        this.results = res.data.collection.items;
        this.loading = false;
        this.step = 1;
      })
      .catch((err) => {
        console.log(err);
      })
    }, 1000),
    
    handleModalOpen(item) {
      this.modalOpen = true
      this.modalData = item
    }
  },

}
</script>

<style lang="less">
@import url("https://fonts.googleapis.com/css2?family=Jost:wght@300&family=Poppins:wght@200;400;700&display=swap");

@wrapper-max-width: 1220px;
@layout-padding: 16px;
@font-family-base: 'Poppins', sans-serif;
@main-color: #466c6e;



body {
  font-family: @font-family-base;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

h1 {
  margin: 0;
}

.page-container {
  height: 100vh;

  .page-wrapper {
    max-width: @wrapper-max-width;
    height: 100%;
    margin: auto;
    padding-left: @layout-padding;
    padding-right: @layout-padding;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;

    &.flexStart {
      align-items: flex-start;
    }

    .content {
      text-align: center;

      &.narrow {
         max-width: 500px;
      }
    }
  }

  .images-container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 20px
  }

  // transitions

  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s ease;
  }

  .fade-enter-from,
  .fade-leave-to {
    opacity: 0;
  }

  .slide-enter-active,
  .slide-leave-active {
    transition: margin-top 0.5s ease;
  }

  .slide-enter-from,
  .slide-leave-to {
    margin-top: -50px;
  }
}

</style>
