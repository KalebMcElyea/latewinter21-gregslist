
<template>
  <div class="house-details m-4">
    <h1>Welcome to this house details page</h1>
    <p>{{ state.house.bedrooms }} Bedrooms {{state.house.bathrooms}} Bathrooms</p>
    <p>{{ state.house.levels}} Levels</p>
    <p> {{state.house.description}}</p>
    <p>$ {{state.house.price}}</p>
    <button type="button" class="btn btn-outline-danger" @click="deleteHouse">
      Delete House
    </button>

  </div>
</template>

<script>
import { reactive } from '@vue/reactivity'
import { useRoute, useRouter } from 'vue-router'
import { computed, onMounted } from '@vue/runtime-core'
import { AppState } from '../Appstate'
import { housesService } from '../services/HousesService'

export default {
  name: 'HouseDetailsPage',
  setup() {
    const route = useRoute()
    const router = useRouter()
    const state = reactive({
      house: computed(() => AppState.activeHouse)
    })

    onMounted(() => {
      housesService.getHouse(route.params.id)
    })

    return {
      route,
      state,
      async deleteHouse() {
        await housesService.deleteHouse(state.house.id)
        router.push({ name: 'Houses' })
      }
    }
  },

  components: {}
}
</script>

<style lang="scss" scoped>
</style>
