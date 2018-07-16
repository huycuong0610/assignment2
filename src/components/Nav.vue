<template>
    <div :class="['nav', data.title]">

        <ul >
          <li v-for="item in data.content" :key="item" @click="changeLocation(item)">  {{ item }}</li>
        </ul>
        
    </div>
</template>

<script>
export default {
  name: 'Nav',
  props: [ 'data', 'changeLocation' ]
}
</script>

<style scoped>

</style>
