<template>
  <form action="/" class="decor">
    <div class="form-wrapper">
      <form v-on:submit.prevent="handleSubmit()" action class="place-form">
      <h2>Add a new place</h2>
      <link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700"
      rel="stylesheet">

      <div class="single-input">
        <label for="name">Place Name:</label>
        <input type="text" id="name" name="name" v-model="name" required />

        <label for="lat">Latitude:</label>
        <input type="number" step="any" id="lat" name="lat" v-model="lat" required />

        <label for="long">Longitude:</label>
        <input type="number" step="any" id="long" name="long" v-model="long" required />

        <label for="type">Type</label>
          <select name="type" id v-model="type">
            <option v-for="(type, index) in types" :key="index">{{type}}</option>
          </select>
      </div>
      <div class="field-input">
        <label for="description">Description:</label>
        <textarea id="description" rows="5" name="description" v-model="description" required></textarea>
      </div>

      <input type="submit" name="submit" value="Save" />
      </form>
    </div>
    <div class="form-left-decoration"></div>
    <div class="form-right-decoration"></div>
    <div class="circle"></div>
    <div class="form-inner">
      <h2>Add Place</h2>
      <input type="text" placeholder="Name of Place">
      <input type="number" placeholder="Latitude">
      <input type="number" placeholder="Longitude">
      <textarea placeholder="Description..." rows="5"></textarea>
      <button type="submit" href="/">Submit</button>
    </div>  

  </form>
    

</template>

<script>
import { eventBus } from "@/main";
import ApiServices from "../services/apiServices.js";

export default {
  data() {
    return {
      name: "",
      lat: 0,
      long: 0,
      description: "",
      type: ""
    };
  },
  name: "place-form",
  props: ["places", "types"],

  methods: {
    handleSubmit() {
      const payload = {
        name: this.name,
        lat: this.lat,
        long: this.long,
        description: this.description,
        type: this.type
      };
      ApiServices.postTreasure(payload).then(res =>
        eventBus.$emit("add-place", res)
      );
      this.name = "";
      this.lat = "";
      this.long = "";
      this.description = "";
      this.type = "";
    }
  }
};
</script>

<style>
.form-wrapper{
  box-sizing:border-box;
  }
html, body{
  box-sizing:border-box;
  min-height: 100vh;
  padding: 0;
  margin: 0;
  font-family:Roboto, Arial, sans-serif;
  font-size: 14px;
  color: #666;
}
input, textarea{
  outline: none;
}
body{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  background: #5a7233;
}
h2{
  margin-top: 0;
  font-weight: 500;
}
.form{
  position: relative;
  width: 80%;
  border-radius: 30px;
  background: #fff;
}
.form-left-decoration, 
.form-right-decoration{
  content: "";
  position: absolute;
  width: 50px;
  height: 20px;
  border-radius: 20px;
  background: #5a7233;
}
.form-left-decoration{
  bottom: 60px;
  left: -30px;
}
.form-right-decoration{
  top: 60px;
  right: -30px;
}
.form-left-decoration:before,
.form-left-decoration:after,
.form-right-decoration:before,
.form-right-decoration:after{
  content: "";
  position: absolute;
  width: 50px;
  height: 20px;
  border-radius: 30px;
  background: #fff;
}
.form-left-decoration:before{
  top: -20px;
}
.form-left-decoration:after{
  top: 20px;
  left: 10px;
}
.form-right-decoration:before{
  top: -20px;
}
.form-right-decoration:after{
  top: 20px;
  right: 10px;
}
.circle{
  position: absolute;
  bottom: 80px;
  left: -55px;
  width: 20px;
  border-radius: 50%;
  background: #fff;
}
.form-inner{
  padding: 40px;
}
.form-inner input,
.form-inner textarea{
  display: block;
  width: 100%;
  padding: 15px;
  margin-bottom: 10px;
  border: none;
  border-radius: 20px;
  background: #d0dfe8;
}
.form-inner textarea{
  resize:none;
}
/* @media(min-width: 568px){
  form{
    width: 60%;
  }
} */
  /* min-height: 100vh;
  padding: 0;
  margin: 0;
  font-family:Roboto, Arial, sans-serif;
  font-size: 14px;
  color: #666;
} */


.single-input {
  /* display: grid;
  grid-template-columns: auto;
  width: 50%; */
}

.field-input {
  /* display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 20vh;
  align-self: center; */
}
</style>