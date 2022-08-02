<template>
  <select @change="changeHandler">
    <option v-for="option in options" :value="option.value" :key="option.value">
      {{ option.text }}
    </option>
  </select>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
    },
  },

  methods: {
    changeHandler(event) {
      this.$emit("selection", event.target.value);
    },
  },
};
</script>
