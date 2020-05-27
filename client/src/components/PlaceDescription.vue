<template lang="html">
    <div class="description-container">
          <div class="description">
            <b>Description:</b>
            {{place.description}}
          </div>

    </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: ["place"]
};
</script>


<style>

.description-container{
  display: flex;
  width: 80%;
  height: 100% ;
  text-align: center;
  background-color: #141C3D ;
  color: #DAFEFF;
  border-radius: 10px;
  font-size: 1.2em;
}

.description{
  width: 60%;
  margin: auto;
  height: auto;
  text-align: justify;
}

</style>