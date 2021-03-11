<template>
  <div class="col-4">
<router-link :to="{name: 'HouseDetailsPage', params: {id: house._id}}" >
  <div class="house-card">
    <img class="card-img-top" :src="house.imgUrl" alt="house">
    <div class="card-body">
      <h3 class="card-title"> {{house.bedrooms}} {{house.bathrooms}}</h3>
      <h5 class="card-text">{{house.level}} {{house.year}}</h5>
      <p class="card-bottom-text">{{house.price}} {{house.imgUrl}}</p>
      <p class="desc">{{house.description}}</p>

    </div>
  </div>
</router-link>
  </div>
</template>

<script>
export default {
  name: 'house',
  props: {
    house: Object
  },
  setup() {
    return {}
  },
  components: {}
}
</script>

<style scoped>
.house:hover {
  transform: translateY(-5px);
  box-shadow: 1px 3px 5px rgb(94, 94, 94);
  cursor: pointer
}

.house {
  transition: all .2s;
  color: black
}
</style>
