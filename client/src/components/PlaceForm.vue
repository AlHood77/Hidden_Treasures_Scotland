<template>
  <div>
    <form v-on:submit.prevent="handleSubmit()" class="form-wrapper">
      
      
        <div class="form-row">
            <div class="col-25">
                <label for="name">Place Name:</label>
            </div>
            <div class="col-75">
                <input type="text" id="name" name="name" v-model="name" required />
            </div>
        </div>

        <div class="form-row">
            <div class="col-25">
                <label for="lat">Latitude:</label>
            </div>
            <div class="col-75">
               <input type="number" step="any" id="lat" name="lat" v-model="lat" required />
            </div>
        </div>

        <div class="form-row">
            <div class="col-25">
                <label for="long">Longitude:</label>
            </div>
            <div class="col-75">
               <input type="number" step="any" id="long" name="long" v-model="long" required />
            </div>
        </div>
        <div class="form-row">
            <div class="col-25">
                <label for="type">Type</label>
            </div>
            <div class="col-75">
               <select name="type" id v-model="type">
                  <option v-for="(type, index) in types" :key="index">{{type}}</option>
               </select>
            </div>
        </div>
        <div class="form-row">
            <div class="col-25">
                <label for="description">Description:</label>
            </div>
            <div class="col-75">
               <textarea id="description" rows="5" name="description" v-model="description" required></textarea>
            </div>
        </div>
        <div class="form-row">
            <input type="submit" name="submit" value="Save" class="submit-button"/>
        </div>
  
    </form>
  </div>
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
  mounted() {
    eventBus.$on('location-selected', latlng => {
      this.lat = latlng.lat
      this.long = latlng.lng
    })
  },

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

<style scoped>

* {
  box-sizing: border-box;
}

input[type=text], [type=number], select, textarea {
  width: 100%;
  padding: 6px;
  border: 1px solid #ccc;
  border-radius: 4px;
  resize: vertical;
}

label {
  padding: 12px 12px 12px 0px;
  display: inline-block;
}

input[type=submit] {
  background-color: #4CAF50;
  color: white;
  padding: 12px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  float: right;
}

input[type=submit]:hover {
  background-color: #45a049;
}

.form-wrapper {
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
  width: 100%;
  height: 100%;
  text-align: center;
}

.col-25 {
  float: left;
  width: 100%;
  margin-top: 6px;
}

.col-75 {
  float: right;
  width: 100%;
}

/* Clear floats after the columns */
.form-row:after {
  content: "";
  display: table;
  clear: both;
}

@media screen and (max-width: 600px) {
  .col-25, .col-75, input[type=submit] {
    width: 100%;
    margin-top: 0;
  }
}

</style>