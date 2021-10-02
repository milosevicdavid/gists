<template>
  <div>
    <div id="app">
      <div>
        <h1 class="title">Github gists</h1>
        <div v-if="loads" class="spinner-loader">
          <p class="loading">Loading...</p>
          <rotate-square3></rotate-square3>
        </div>
        <div v-else class="items-buttons">
          <div class="buttons">
            <button @click="getItems(1)">1</button>
            <button @click="getItems(2)">2</button>
          </div>
          <Gist v-for="item in gist" :key="item.id" :item="item" />
          <div class="buttons">
            <button @click="getItems(1)">1</button>
            <button @click="getItems(2)">2</button>
            <button @click="windowTop">↑</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Gist from "./components/Gist.vue";
import { RotateSquare3 } from "vue-loading-spinner";

export default {
  name: "App",
  components: {
    Gist,
    RotateSquare3
  },
  data() {
    return {
      gist: [],
      page: "",
      loads: false,
      click: 1
    };
  },

  mounted() {
    this.getItems();
  },

  methods: {
    getItems(num = 1) {
      this.loads = true;
      fetch(`https://api.github.com/gists/public?page=${num}`)
        .then(response => response.json())
        .then(data => (this.gist = data))
        .then(() => (this.loads = false));

      this.windowTop();
    },
    windowTop() {
      window.scroll(0, 0);
    }
  }
};
</script>

<style>
html {
  scroll-behavior: smooth;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
}

.title {
  text-align: center;
}

.buttons {
  display: flex;
  justify-content: center;
  align-items: center;
}

.buttons button {
  margin: 20px 5px;
  color: #177ef2;
  width: 40px;
  height: 40px;
  border: 1px solid #177ef2;
  background-color: white;
  cursor: pointer;
}

.buttons button:hover {
  color: gray;
  border: 1px solid gray;
}

.spinner-loader {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  height: 200px;
  margin-top: 200px;
  font-size: 24px;
}

.spinner {
  width: 80px !important;
  height: 80px !important;
}

.loading {
  color: #4fc08d;
}

.items-buttons {
  margin-top: 120px;
}
</style>
