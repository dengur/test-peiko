<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/peiko-logo-mini.png">
    <h1>Test</h1>
    <hr>
    <button class="btn" @click="loadData">Get data</button>
    <Table v-if="data !== null" :data="data"/>
    <p v-else>{{ loaded ? 'No data' : 'Loading...' }}</p>
  </div>
</template>

<script>
import {payload} from "@/mocData";
import getDataFunc from "@/plugins/getDataFunc";
import Table from '@/components/table/Table'

export default {
  name: 'App',
  components: {
    Table
  },
  data() {
    return {
      data: null,
      loaded: false
    }
  },
  methods: {
    reset() {
      this.data = null
      this.loaded = false
    },
    async loadData() {
      this.reset()
      try {
        this.data = await getDataFunc(payload);
        this.loaded = true
      } catch (error) {
        this.loaded = true
        console.error('Error:', error)
      }
    }
  },
  created() {
    this.loadData()
  }
}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.btn {
  margin-top: 20px;
  margin-bottom: 17px;
  padding: 5px 10px;
  background-color: #F5F5F5;
  border: 1px solid #EEEEEE;
  max-width: 115px;
  width: 100%;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;

  &:hover {
    background-color: #EEEEEE;
  }

  &:focus {
    background-color: #ECEAEA;
  }
}
</style>
