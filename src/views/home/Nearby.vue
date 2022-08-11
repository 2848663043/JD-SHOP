<template>
  <div class="nearby">
    <h3 class="nearby__title">附近店铺</h3>
     <!-- <suspense>
       <template #default> -->
    <router-link
      v-for="item in nearbyList"
      :key="item._id"
      :to="`/shop/${item._id}`"
    >  
      <ShopInfo :item="item" />
    </router-link>
    <!-- </template>
    <template #fallback>
      Loading ...
    </template>
    </suspense> -->
  </div>
</template>

<script setup name="Nearby">
import { ref   } from 'vue'
import { get } from '../../utils/request'
import ShopInfo from '../../components/ShopInfo'
// const useNearbyListEffect = () => {
//   const nearbyList = ref([]);
//   const getNearbyList = async () => {
//     const result = await get('/api/shop/hot-list')
//     console.log(result)
//     if (result?.errno === 0 && result?.data?.length) {
//       nearbyList.value = result.data
//     }
//   }
//   return { nearbyList, getNearbyList}
// }

// export default {
//   name: 'Nearby',
//   
//   setup() {
//     const { nearbyList, getNearbyList } = useNearbyListEffect();
//     getNearbyList();
//     return { nearbyList };
//   }
// }

  const nearbyList = ref([]);
  const getNearbyList = async () => {
    const result = await get('/api/shop/hot-list')
    if (result?.errno === 0 && result?.data?.length) {
      nearbyList.value = result.data
    }   
  }
  getNearbyList()
</script>

<style lang="scss" scoped>
@import '../../style/viriables.scss';
.nearby {
  &__title {
    margin: .16rem 0 .02rem 0;
    font-size: .18rem;
    font-weight: normal;
    color: $content-fontcolor;
  }
  a {
    text-decoration: none;
  }
}
</style>