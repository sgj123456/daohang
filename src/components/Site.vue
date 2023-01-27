<script setup>
import { ref } from 'vue';
defineProps(["title", "data"]);
defineEmits(["urlClick"])
const urlshow = ref(false)
</script>

<template>
    <div v-if="Object.keys(data.url).length == 1 && data.introduce == '' ? false : true">
        <el-button v-text="title" :name="title" @click="urlshow = !urlshow"></el-button>
        <div v-if="urlshow" id="url" style="background-color: #66ccff66 !important;">
            <strong v-text="data.introduce" v-if="data.introduce!==''"></strong>
            <el-button v-for="(value, key, index) of data.url" v-text="key" @click="$emit('urlClick', key, value)"
                :key="index"></el-button>
        </div>
    </div>
    <div v-else>
        <el-button v-text="title"
            @click="$emit('urlClick', Object.keys(data.url)[0], data.url[Object.keys(data.url)[0]])"></el-button>
    </div>
</template>

<style scoped>
button {
    position: relative;
    width: 10rem;
    margin-left: 0 !important;
}

#url {
    display: block;
    position: absolute;
    background-color: white !important;
    width: 70% !important;
    z-index: 1;
    left: 50%;
    transform: translate(-50%, 0%);
}
</style>
