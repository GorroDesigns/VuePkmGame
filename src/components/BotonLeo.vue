<template>
  <button @click="$emit('click-boton')">
    {{ leyenda }}
  </button>
</template>

<script>
export default {
  props: {
    leyenda: {
      type: String,
      default: "Btn",
    },
  },
};
</script>

