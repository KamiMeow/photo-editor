<template>
  <div class="loader-section">
    <div v-for="image in images" :key="image.name" class="loader-section__loaded-images">
      <image-view :data="image.data" :name="image.name" @select="selectImage(image)" />
    </div>

    <div class="loader-section__loader-section">
      <loader :data="dataComp" />
    </div>
  </div>
</template>

<script>
import ImageView from './imageView.vue';
import Loader from './loader.vue';
import axios from 'axios';

export default {
  name: 'Download',
  components: {
    ImageView,
    Loader,
  },
  props: {
    data: {
      type: Object,
      default: () => ({}),
    },
  },
  created() {
    this.loadPhotos();
  },
  data: () => ({
    images: [],
  }),
  computed: {
    dataComp: {
      get() {
        return this.data;
      },
      set(data) {
        this.updateData(data);
      },
    },
  },
  methods: {
    updateData(data) {
      Object.assign(this.data, data);
    },

    selectImage(image) {
      this.updateData({
        name: image.name,
        data: image.data,
        url: image.data,
        loaded: true,
      })
    },

    async loadPhotos() {
      this.images = (await axios.get('http://localhost:3000/photos')).data;
    },
  },
};
</script>

<style>
  .loader-section {
    width: 100%;
    height: 100%;
    padding: 25px;
    display: flex;
    justify-items: center;

    overflow-x: scroll;
  }
  .loader-section__loader-section,
  .loader-section__loaded-images {
    padding: 5px;
  }
</style>