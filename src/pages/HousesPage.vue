<template>
  <div class="houses-page container ">
    <h1 class="text-center">Houses</h1>
    <form class="form-inline" @submit.prevent="createHouse">
      <div class="form-group m-1">
        <input
          type="text"
          name="bedroom"
          id="bedrooms"
          class="form-control"
          placeholder="Bedrooms"
          aria-describedby="helpId"
          v-model="state.house.bedrooms"
        />
      </div>
      <div class="form-group m-1">
        <input
          type="text"
          name="bathrooms"
          id="bathrooms"
          class="form-control"
          placeholder="Bathrooms"
          aria-describedby="helpId"
          v-model="state.house.bathrooms"
        />
      </div>
      <div class="form-group m-1">
        <input
          type="number"
          name="levels"
          id="levels"
          class="form-control"
          placeholder="Levels"
          aria-describedby="helpId"
          v-model="state.house.levels"
        />
      </div>
      <div class="form-group m-1">
        <input
          type="number"
          name="price"
          id="price"
          class="form-control"
          placeholder="Price"
          aria-describedby="helpId"
          v-model="state.house.price"
        />
      </div>
      <div class="form-group m-1">
        <input
          type="text"
          name="description"
          id="description"
          class="form-control"
          placeholder="Description"
          aria-describedby="helpId"
          v-model="state.house.description"
        />
      </div>
      <div class="form-group m-1">
        <input
          type="number"
          name="year"
          id="year"
          class="form-control"
          placeholder="Year"
          aria-describedby="helpId"
          v-model="state.house.year"
        />
      </div>
      <div class="form-group m-1">
        <input
          type="text"
          name="imgUrl"
          id="imgUrl"
          class="form-control"
          placeholder="ImgUrl"
          aria-describedby="helpId"
          v-model="state.house.imgUrl"
        />
      </div>
      <button class="btn btn-info" type="submit">Create</button>
    </form>
  </div>
  <div class="row">
    <House v-for="houseData in state.houses" :key="houseData._id" :house="houseData" />
  </div>
</template>

<script>
import { reactive, computed, onMounted } from '@vue/runtime-core'
import { AppState } from '../Appstate'
import { housesService } from '../services/HousesService'
import House from '../components/House'
import { useRouter } from 'vue-router'

export default {
  name: 'HousesPages',
  setup() {
    const router = useRouter()
    const state = reactive({
      houses: computed(() => AppState.houses),
      house: {}

    })

    onMounted(() => {
      housesService.getHouses()
    })

    return {
      state,
      async createHouse() {
        const houseId = await housesService.createHouse(state.house)
        router.push({ name: 'HouseDetails', params: { id: houseId } })
        state.newHouse = {}
      }
    }
  },

  components: {
    House
  }
}

</script>

<style lang="scss" scoped>

</style>
