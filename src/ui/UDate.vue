<template>
  <label class="uidate">
    <span class="uidate__label">{{ label }}</span>
    <input
      :value="value"
      @input="$emit('input', $event.target.value)"
      class="uidate__field"
      type="date"
    />
    <span class="error">{{ getError }}</span>
  </label>
</template>

<script>
export default {
  props: {
    value: String,
    label: String,
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
.uidate {
  display: flex;
  flex-direction: column;
  height: 38px;
  &__label {
    font-size: 12px;
    padding: 0 0 4px 4px;
    font-weight: bold;
  }

  &__field {
    font-size: 1.1rem;
    min-height: 100%;
    padding: 6px 12px;
    border: 1px solid #cccccc;
    outline: none;
  }
}

.error {
  font-size: 10px;
  padding-left: 8px;
  padding-top: 4px;
  color: red;
  font-weight: bold;
  min-height: 12px;
}
</style>
