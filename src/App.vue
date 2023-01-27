<script setup>
import Site from './components/Site.vue';
import data from '../public/data.json'
import { ref } from 'vue';
const sitedata = ref({ "工口专区": {}, "软件专区": {}, "编程专区": {}, "搞机专区": {}, "搜索导航": {}, "影音阅读": {}, "VPN专区": {} })
Object.keys(data).forEach(element => {
  sitedata.value[data[element]["classify"]][element] = data[element]
})
const zhanshi = ref({})
function guanbi() {
  zhanshi.value = {}
}
function click(urlkey, urlvalue) {
  if (typeof urlvalue == "string") {
    console.log(urlvalue);
    open(urlvalue)
  } else {
    zhanshi.value["key"] = urlkey
    zhanshi.value["value"] = urlvalue
  }
}
function openurl(url) {
  open(url)
}
</script>

<template>
  <div id="zhanshi" v-if="Object.keys(zhanshi).length !== 0" style="background-color: #66ccffaa;">
    <el-button @click="guanbi" id="guanbi">关闭</el-button>
    <strong v-text="zhanshi.value.introduce"></strong>
    <el-button @click="openurl(zhanshi.value.url)" v-text="zhanshi.key"></el-button>
  </div>
  <el-card v-for="(sites, key, index) of sitedata" :key="index" class="box-card" style="width: 250px">
    <template #header>
      <div>
        <span v-text="key"></span>
      </div>
    </template>
    <Site v-for="(value, key, index) of sites" :title="key" :data="value" @url-click="click" :key="index"></Site>
  </el-card>
</template>

<style scoped>
.el-card {
  width: 100% !important;
}
#guanbi{
  position: fixed;
  right: 0;
}
#zhanshi {
  margin-top: 80%;
  background-color: white;
  position: fixed;
  top: 0;
  width: 100%;
  height: 100%;
  z-index: 10;
}
</style>
