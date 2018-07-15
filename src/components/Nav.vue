<template>
    <div :class="['tile', data.title]">

        <ul v-for="item in data.content" :key="item">
          <li @click="changeLocation(item)">  {{ item }}</li>
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
