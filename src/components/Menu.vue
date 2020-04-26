<template>
  <div id="menu">
        <input type="text" v-model="range.x">
        <input type="text" v-model="range.y">
        <button @click="$emit('togglePlay')">Play</button>
    </div>
</template>

<script>
export default {
    props: ['range','play']
}
</script>

<style>

</style>