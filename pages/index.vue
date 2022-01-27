<template>
  <div>
    <div class="banner">
      <img :src="response.details.ext_col_01.url" />
      <div class="banner_text">
        <h1>{{ response.details.ext_col_02 }}</h1>
        <p>{{ response.details.ext_col_03 }}</p>
      </div>
    </div>

    <h2>WORKS</h2>
    <div v-for="n in response.details.ext_col_04" :key="n.slag" class="works">
      <img :src="n.ext_col_04.url" />
      <div>
        <div class="works_title">{{ n.ext_col_05 }}</div>
        <div class="works_text">{{ n.ext_col_06 }}</div>
      </div>
    </div>

    <h2>ABOUT</h2>
    <div class="about">
      <div class="about_text" v-html="response.details.ext_col_07"></div>
    </div>
  </div>
</template>

<style>
.banner {
  position: relative;
}
.banner img {
  width: 100%;
}
.banner_text {
  width: 45%;
  position: absolute;
  text-align: right;
  top: 30%;
  right: 5%;
  bottom: 20%;
}
.banner_text p {
  font-size: 1.5rem;
}
.title_text p {
  width: 100%;
}
.works {
  display: flex;
  margin-right: 30px;
  margin-left: 30px;
}
.works_title {
  margin-top: 50px;
  font-size: 3rem;
}
.works_text {
  width: 90%;
  font-size: 1.5rem;
}
.works img {
  width: 400px;
  padding: 50px;
}
.about {
  display: flex;
  justify-content: center;
  margin: 30px;
}
.about_text {
  margin-right: 200px;
  margin-left: 200px;
  font-size: 1.5rem;
}
h1 {
  font-size: 3rem;
}
h2 {
  text-align: center;
  font-size: 3.5rem;
  margin-top: 100px;
}
</style>

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