<template>
    <section>
      <fieldset>
          <legend>
            Address Lookup
          </legend>
          <div>
            <label for="postcodeLookup">Enter postcode</label>
            <input id="postcodeLookup" v-model="postcode" type="text" placeholder="Enter postcode">
            <button v-on:click="addressLookUp">Search Postcode</button>
          </div>
      </fieldset>
      <fieldset v-if="postCodeSearched">
        <legend>Select your address</legend>
        <select v-model="selectedAddress" v-on:change="emitAddress">
          <option value='' selected>Please select</option>
          <option :value="item" v-for="(item, index) in addressList" :key="index">{{item}}</option>
        </select>
      </fieldset>
      <p v-if="noResults">Sorry, we were unable to find that post-code</p>
    </section>
</template>

<script>
import axios from 'axios';

export default {
  name: 'AddressLookUp',
  data() {
    return {
      isSearching: false,
      postcode: '',
      addressList: [],
      selectedAddress: '',
      postCodeSearched: false,
      noResults: false
    }
  },
  methods: {
    addressLookUp() {
      axios.get(`https://api.getAddress.io/find/${this.postcode}?api-key={add key here}`)
        .then(response => { 
              this.addressList = response.data.addresses
              this.postCodeSearched = true
              this.noResults = false
         })
        .catch(error => {
          this.noResults = true
          console.log(error);
        })
    },
    emitAddress() {
      if(this.selectedAddress != '') {
        this.$emit('addressChanged', this.selectedAddress)
      }
    }
  }
}
</script>
