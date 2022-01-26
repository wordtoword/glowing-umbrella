<template>
  <div>
    <img :src="response.details.ext_col_01.url" width="800">
    <div>{{response.details.ext_col_02}}</div>
    <div>{{response.details.ext_col_03}}</div>

    <div v-for="n in response.details.ext_col_04" :key="n.slag" >
      <img :src="n.ext_col_04.url" width="400">
      <div>{{ n.ext_col_03 }}</div>
      <div>{{ n.ext_col_05 }}</div>
      <div>{{ n.ext_col_06 }}</div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, app }) {
    try {
      const response = await $axios.$get(
        process.env.BASE_URL + '/rcms-api/3/service/3'
        )
        console.log(response)
        return { response }
        } catch (e) {
          console.log(e.message)
          }
  },
}
</script>