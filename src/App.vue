<template>
  <div id="app">
    <post-code-look-up v-on:addressChanged="updateAddress"></post-code-look-up>
    <fieldset>
      <legend>Your address</legend>
      <div>
          <label for="house">House/Flat Number</label>
          <input id="house" v-model="house" placeholder="House/Flat Number">
      </div>
      <div>
          <label for="building">Building</label>
          <input id="building" v-model="building" placeholder="Building">
      </div>
      <div>
          <label for="street">Street</label>
          <input id="street" v-model="street" placeholder="Street">
      </div>
      <div>
          <label for="suburb">Suburb</label>
          <input id="suburb" v-model="suburb" placeholder="Suburb">
      </div>
      <div>
          <label for="city">City</label>
          <input id="city" v-model="city" placeholder="City">
      </div>
    </fieldset>
  </div>
</template>

<script>
import PostCodeLookUp from './components/PostCodeLookUp'
export default {
  name: 'app',
  components: {
    PostCodeLookUp
  },
  data() {
    return {
      house: '',
      building: '',
      street: '',
      suburb: '',
      city: '',
    }
  },             
  methods: {
    updateAddress(payLoad) {   
        let addressArray = payLoad.split(",")
        this.house = addressArray[0]
        this.building = addressArray[1]
        this.street = addressArray[2]
        this.suburb = addressArray[4]
        this.city = addressArray[5]
      }
    }
  }
</script>

<style>
fieldset {
  display: flex;
  flex-flow: row;
  align-items: center;
  justify-content: center;
}
fieldset > div {
    display: inline-flex;
    align-items: center;
    margin-bottom: 10px;
}
input, select {
  border: 1px solid #ccc;
  padding: 10px;
}
label {
  width: 20%;
}
</style>
