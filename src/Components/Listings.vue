<template>
  <div class="listings">
    <h1>Listings</h1>

    <label for="sortBy">Sort by</label>
    <select id="sortBy" v-model="sort">
      <option value="newest">Latest Listings</option>
      <option value="price">Lowest Price</option>
      <option value="distance">Distance to Western</option>
    </select>

    <listing
      v-for="(listing, index) in sortedListings"
      v-bind:listing="listing"
      v-bind:index="index">
    </listing>
  </div>
</template>

<script>
import Listing from './Listing.vue'

function sortBy (array, key) {

  switch (key) {
    case 'newest':
      return array.sort((a, b) => {
        return a.posted - b.posted
      })
      break;
    case 'price':
      return array.sort((a, b) => {
        return a.rent - b.rent
      })
    case 'distance':
      return array.sort((a, b) => {
        return a.distance - b.distance
      })
    default:
      return array
  }
}

export default {
  components: {
    Listing
  },

  data () {
    return {
      listings: require('../assets/listings'),
      sort: 'newest'
    }
  },

  computed: {
    sortedListings () {
      return sortBy(this.listings, this.sort)
    }
  }
}
</script>

<style>
</style>
