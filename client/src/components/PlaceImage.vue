<template>
  <div>
    <img
      :src="this.place.url"
      alt="Invalid Url"
      crossorigin="anonymous"
      class="image"
    />
  </div>
</template>

<script>
export default {
  name: "place-container",
  props: ['place']
};
</script>

<style scoped>

/* div{
  align-items: center;
} */

.image {
  width: 30vw;
}
</style>