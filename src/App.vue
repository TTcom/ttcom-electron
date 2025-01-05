<script setup>
// import HelloWorld from './components/HelloWorld.vue'
import {ref} from 'vue'
let result = ref('')
async function toload(){
  const filePath = '/githubproject/electron-vite-vue-main/src/components/data.json';
  let data = await window.electronAPI.readJsonFile(filePath);
  console.log('dataaaaaaaa',data)
  result.value = data.list
}
async function tochange(){
  result.value.push({name:'老李',age:'36'})
  let jsonData ={"list":result.value}
// 将修改后的数据发送到主进程，并保存到文件
const filePath = '/githubproject/electron-vite-vue-main/src/components/data.json';
await window.electronAPI.writeJsonFile(filePath, JSON.stringify(jsonData));
}



</script>

<template>
  <div>
    <div @click="toload"> 
      loadfiledata
    </div>
    <div style="margin: 100px 0;" @click="tochange"> 
      changeData
    </div>
    <div v-for="(item,i) in result">
         {{item.name}} && {{item.age}}
    </div>
    <!-- <a href="https://www.electronjs.org/" target="_blank">
      <img src="./assets/electron.svg" class="logo electron" alt="Electron logo" />
    </a>
    <a href="https://vitejs.dev/" target="_blank">
      <img src="./assets/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Electron + Vite + Vue" />
  <div class="flex-center">
    Place static files into the <code>/public</code> folder
    <img style="width: 2.4em; margin-left: .4em;" src="/logo.svg" alt="Logo">-->
  </div> 
</template>

<style>
.flex-center {
  display: flex;
  align-items: center;
  justify-content: center;
}

.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo.electron:hover {
  filter: drop-shadow(0 0 2em #9FEAF9);
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
