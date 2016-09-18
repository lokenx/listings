<template>
  <div class="listing">
    <h3>{{ this.listing.address }} - ${{ this.listing.rent }}</h3>
    <h4>{{ postedDate }}</h4>
    <h4>{{ this.listing.distance }}km</h4>
    <ul>
      <div v-for="(value, key) in this.listing">
        <li v-if="value">{{ key }}: {{ value }}</li>
      </div>
    </ul>
  </div>
</template>

<script>
import Moment from 'moment'

export default {
  props: {
    listing: Object,
    index: Number
  },

  computed: {
    postedDate: function () {
      return Moment.unix(this.listing.posted).format('MMMM Do YYYY');
    }
  }
}
</script>

<style>
</style>
