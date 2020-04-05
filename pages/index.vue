<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">prueba-rebecca-purple</h1>
      <h2 class="subtitle">Prueba de programacion de Rebecca Purple</h2>
    </div>
    <h3 class="list-title">Lista de productos:</h3>
    <div class="list">
      <span v-if="error != ''" class="error">{{ error }}</span>
      <ol v-else>
        <li v-for="item in list.slice(0, 15)" :key="item.id">
          {{ item.name }},
          <small v-if="item.statusId == 1" style="color: blue"
            >Estado: Pago aceptado</small
          >
          <small v-if="item.statusId == 2" style="color: salmon"
            >Estado: Pago rechazado</small
          >
          <small v-if="item.statusId == 3" style="color: limegreen"
            >Estado: Sincronizado</small
          >
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  data() {
    return {
      list: [],
      error: ''
    }
  },
  async created() {
    try {
      this.list = await this.$axios.$get(
        // 'https://jsonplaceholder.typicode.com/albums',
        'http://localhost:3001/status/3/products',
        // 'http://localhost:80/prueba/api/products/?ws_key=L729B1GR3ZK4K9KHML2BP6D65NXUZ3SM',
        // 'http://L729B1GR3ZK4K9KHML2BP6D65NXUZ3SM@localhost:80/prueba/api/products/,'
        // 'http://L729B1GR3ZK4K9KHML2BP6D65NXUZ3SM@localhost:80/prueba/api/products/?output_format=JSON',
        {
          headers: {
            'Access-Control-Allow-Origin': '*',
            'Content-type': 'application/json'
          }
        }
      )
    } catch (error) {
      this.error = error
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  min-width: 100vw;
  display: block;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.list {
  text-align: left;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 40px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 26px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.list-title {
  font-weight: 300;
  font-size: 22px;
  color: #526488;
  word-spacing: 5px;
  text-decoration: underline;
}

.error {
  color: salmon;
}
</style>
