<template>
  <div class="listings">
    <h1>Listings</h1>

    <label for="sortBy">Sort by</label>
    <select id="sortBy" v-model="sort">
      <option value="newest">Latest Listings</option>
      <option value="price">Lowest Price</option>
      <option value="distance">Distance to Western</option>
    </select>

    <label for="filterByType">Filter by type</label>
    <select id="filterByType" v-model="filters.type">
      <option>Any</option>
      <option>Student</option>
      <option>Graduate Student</option>
    </select>

    <label for="filterByLocation">Filter by location</label>
    <select id="filterByLocation" v-model="filters.location">
      <option>Any</option>
      <option>Downtown</option>
      <option>Old North</option>
      <option>Old South</option>
      <option>On Campus</option>
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
      sort: 'newest',
      filters: {
        type: 'Any',
        location: 'Any'
      }
    }
  },

  computed: {
    filteredListings() {
      const filter = JSON.parse(JSON.stringify(this.filters))

      return this.listings.filter((item) => {

        for(let key in filter) {
          if (item[key] !== filter[key] && filter[key] !== 'Any') {
            return false
          }
        }
        return true
      })
    },
    sortedListings () {
      return sortBy(this.filteredListings, this.sort)
    }
  }
}
</script>

<style>
</style>
