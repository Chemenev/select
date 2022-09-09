<template>
  <input
    type="text"
    ref="input"
    :value="modelValue"
    :placeholder="placeholder"
    @input="input"
    @click="addDropClass"
  />
</template>
<script>
export default {
  data() {
    return {
      positionClass: 'bottom',
    };
  },
  props: {
    modelValue: {
      type: String,
    },
    placeholder: {
      type: String,
    },
  },

  methods: {
    input() {
      this.$emit('update:modelValue', event.target.value);
    },
    addDropClass() {
      const inputPosition = this.$refs.input.getBoundingClientRect();
      if (inputPosition.top >= window.innerHeight - 200) {
        this.positionClass = 'top';
      }
      this.$emit('drop-element', this.positionClass);
      return this.positionClass;
    },
  },
};
</script>
<style scoped>
input {
  border: none;
  padding: 8px 0;
  font-size: 16px;
  outline: none;
}
</style>
