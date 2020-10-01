<template>
  <v-card
    class="mx-auto pa-4 black secondary--border secondary--text"
    :style="{}"
    tile
    :max-width="maxWidth"
    :class="classProp"
    outlined
  >
    <div class="card-title">
      <slot name="title"></slot>
    </div>
    <slot name="body"></slot>
  </v-card>
</template>

<script>
export default {
  name: "BashTopLayout",
  props: {
    maxWidth: {
      type: Number,
      default: undefined
    },
    classProp: {
      type: String,
      default: ''
    }
  }
};
</script>

<style scoped>
.card-title {
  position: absolute;
  top: -12px;
  background: black;
  padding: 0 5px;
}
</style>
