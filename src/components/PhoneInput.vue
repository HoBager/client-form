<template>
  <label class="phone">
    <span class="phone__label">{{ label }}</span>
    <input type="text" :value="value" @input="handleInput($event)" />
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
  watch: {
    value() {
      this.$emit("input", this.value.replace(/[^+\d]/g, ""));
    },
  },
  methods: {
    handleInput(event) {
      const phoneNumber = event.target.value;
      this.$emit("input", `+7 ${phoneNumber.slice(2, 12)}`);
    },
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
.phone {
  display: flex;
  flex-direction: column;

  &__label {
    font-size: 12px;
    padding: 0 0 4px 4px;
    font-weight: bold;
  }
}

.phone input {
  height: 38px;
  padding: 6px 12px;
  border: 1px solid #cccccc;
  outline: none;
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
