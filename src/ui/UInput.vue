<template>
  <label class="uinput">
    <span class="uinput__label">{{ label }}</span>
    <input
      @input="$emit('input', $event.target.value)"
      class="uinput__field"
      type="text"
      :placeholder="placeholder"
      :value="value"
    />
    <span class="error">{{ getError }}</span>
  </label>
</template>

<script>
export default {
  props: {
    placeholder: String,
    label: String,
    value: String,
    error: Array,
  },
  computed: {
    getError() {
      if (this.error && this.error.length) {
        return this.error[0].$message;
      }
      return "";
    },
  },
};
</script>

<style lang="scss" scoped>
.uinput {
  display: flex;
  flex-direction: column;
  &__field {
    height: 38px;
    padding: 6px 12px;
    border: 1px solid #cccccc;
    outline: none;
  }

  &__label {
    font-size: 12px;
    padding: 0 0 4px 4px;
    font-weight: bold;
  }
}

.error {
  font-size: 10px;
  padding-left: 4px;
  padding-top: 4px;
  color: red;
  font-weight: bold;
  min-height: 12px;
}
</style>
