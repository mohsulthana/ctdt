<template>
    <v-card class="mt-4" :to="link">
      <v-card-text class="text-h5 font-weight-bold" style="overflow-y: auto; height:15rem">
        <div class="title">{{ title }}</div>
        <div class="subtitle">{{ subtitle }}</div>
      </v-card-text>
    </v-card>
</template>

<script>
export default {
  props: ['title', 'subtitle', 'link']
}
</script>

<style scoped>
.v-card__text {
    text-align: center;
}

.v-card__text > .title {
  background-color: #0e2d61;
  color: white;
  border-radius: 4px;
  margin: 10px;
  text-align: center;
}
</style>