<template>
  <div class="image-view">
    <img
      :src="data"
      :alt="name"
      class="image-view__image"
      ref="image"
      @click="$emit('select')"
    >
    <div class="image-view__text">
      Load image
    </div>
  </div>
</template>

<script>
export default {
  name: 'imageView',
  props: {
    data: String,
    name: String,
  },
};
</script>

<style>
  .image-view {
    width: 500px;
    height: 300px;
    border: 2px solid black;
    opacity: 1;
    transition: .2s;
    cursor: pointer;
    position: relative;
  }
  .image-view .image-view__text {
    opacity: 0;
    transition: .2s;
  }
  .image-view:hover {
    opacity: 0.4;
    transition: .4s;
  }
  .image-view:hover .image-view__text {
    opacity: 1;
    transition: .4s;
  }

  .image-view__text {
    color: white;
    position: absolute;
    top: 42%;
    left: 35%;
    font-size: 35px;
  }
  .image-view__image {
    width: 100%;
    height: 100%;
  }
</style>