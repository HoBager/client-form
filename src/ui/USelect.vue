<template>
  <div class="form_label">
    <span v-if="label" class="form_text">{{ label }}</span>
    <div class="multiselect_block">
      <label for="select-1" class="field_multiselect">{{ value }} </label>

      <input :id="selectId" class="multiselect_checkbox" type="checkbox" />
      <label :for="selectId" class="multiselect_label"></label>

      <select
        @change="handleChange($event)"
        ref="selectRef"
        id="select-1"
        class="field_select"
        name="technology"
        multiple
      >
        <option v-for="option in options" :value="option" :key="option">
          {{ option }}
        </option>
      </select>
    </div>
    <span class="error_text">{{ getError }}</span>
  </div>
</template>

<script>
export default {
  props: {
    label: String,
    placeholder: String,
    options: Array,
    error: Array,
    value: String,
  },
  data() {
    return { selectId: Date.now() };
  },
  computed: {
    getError() {
      if (this.error && this.error.length) {
        return this.error[0].$message;
      }
      return "";
    },
  },
  methods: {
    handleChange(event) {
      const currentValue = event.target.value;
      for (let option of event.target.options) {
        if (option.value !== currentValue) {
          option.selected = false;
        }
      }

      this.$emit("input", currentValue);
    },
  },
};
</script>

<style lang="scss" scoped>
$red: #eb5757;
$red-hover: #fe130b;

$orange: #ff8964;
$orange-hover: #ff8964;
$orange-disabled: rgba(255, 137, 100, 0.8);

.form_label {
  position: relative;
  min-height: 88px;
}

.form_text {
  vertical-align: top;
  display: block;
  padding-bottom: 3px;
  font-weight: 500;
  line-height: 16px;
  letter-spacing: 0.04em;
  font-size: 12px;
}

.form_label input,
.field_multiselect {
  position: relative;
  width: 100%;
  display: flex;
  align-items: center;
  min-height: 46px;
  font-weight: bold;
  border: 1px solid #cccccc;
  box-sizing: border-box;

  padding: 12px 40px 10px 8px;
  font-size: 12px;

  outline-color: #cdd6f3;

  &::placeholder {
    color: #a8acc9;
  }
  &:hover {
    box-shadow: 0 0 2px rgba(0, 0, 0, 0.16);
  }
  &:focus {
    box-shadow: 0 0 2px rgba(0, 0, 0, 0.16);
  }
}

.form_label input.error {
  border-color: $red;
}

.error_text {
  font-size: 10px;
  padding-left: 8px;
  padding-top: 4px;
  color: red;
  font-weight: bold;
  min-height: 12px;
}

.field_multiselect {
  padding-right: 60px;
  &:after {
    content: "";
    position: absolute;
    right: 14px;
    top: 15px;
    width: 6px;
    height: 16px;
    background: url("data:image/svg+xml,%3Csvg width='6' height='16' viewBox='0 0 6 16' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M3 0L6 5H0L3 0Z' fill='%23A8ACC9'/%3E%3Cpath d='M3 16L6 11H0L3 16Z' fill='%23A8ACC9'/%3E%3C/svg%3E")
      50% 50% no-repeat;
  }
}

.multiselect_block {
  position: relative;
  width: 100%;
}
.field_select {
  position: absolute;
  top: calc(100% - 2px);
  left: 0;
  width: 100%;

  border: 2px solid #cdd6f3;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
  box-sizing: border-box;
  outline-color: #cdd6f3;
  z-index: 6;
}

.field_select {
  overflow-y: auto;
}

.field_select option {
  display: block;
  padding: 8px 16px;

  cursor: pointer;
  &:checked {
    background-color: #eceff3;
  }
  &:hover {
    background-color: #d5e8fb;
  }
}

.field_multiselect button {
  position: relative;
  padding: 7px 34px 7px 8px;
  background: #ebe4fb;
  border-radius: 4px;
  margin-right: 9px;

  &:hover,
  &:focus {
    background-color: #dbd1ee;
  }
  &:after {
    content: "";
    position: absolute;
    top: 7px;
    right: 10px;
    width: 16px;
    height: 16px;
    background: url("data:image/svg+xml,%3Csvg width='24' height='24' viewBox='0 0 24 24' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath fill-rule='evenodd' clip-rule='evenodd' d='M19.4958 6.49499C19.7691 6.22162 19.7691 5.7784 19.4958 5.50504C19.2224 5.23167 18.7792 5.23167 18.5058 5.50504L12.5008 11.5101L6.49576 5.50504C6.22239 5.23167 5.77917 5.23167 5.50581 5.50504C5.23244 5.7784 5.23244 6.22162 5.50581 6.49499L11.5108 12.5L5.50581 18.505C5.23244 18.7784 5.23244 19.2216 5.50581 19.495C5.77917 19.7684 6.22239 19.7684 6.49576 19.495L12.5008 13.49L18.5058 19.495C18.7792 19.7684 19.2224 19.7684 19.4958 19.495C19.7691 19.2216 19.7691 18.7784 19.4958 18.505L13.4907 12.5L19.4958 6.49499Z' fill='%234F5588'/%3E%3C/svg%3E")
      50% 50% no-repeat;
    background-size: contain;
  }
}

.multiselect_label {
  position: absolute;
  top: 1px;
  left: 2px;
  width: 100%;
  height: 44px;
  cursor: pointer;
  z-index: 3;
}

.field_select {
  display: none;
}

input.multiselect_checkbox {
  position: absolute;
  right: 0;
  top: 0;
  width: 40px;
  height: 40px;
  border: none;
  opacity: 0;
}

.multiselect_checkbox:checked ~ .field_select {
  display: block;
}

.multiselect_checkbox:checked ~ .multiselect_label {
  width: 40px;
  left: initial;
  right: 4px;
  background: #ffffff
    url("data:image/svg+xml,%3Csvg width='24' height='24' viewBox='0 0 24 24' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath fill-rule='evenodd' clip-rule='evenodd' d='M19.4958 6.49499C19.7691 6.22162 19.7691 5.7784 19.4958 5.50504C19.2224 5.23167 18.7792 5.23167 18.5058 5.50504L12.5008 11.5101L6.49576 5.50504C6.22239 5.23167 5.77917 5.23167 5.50581 5.50504C5.23244 5.7784 5.23244 6.22162 5.50581 6.49499L11.5108 12.5L5.50581 18.505C5.23244 18.7784 5.23244 19.2216 5.50581 19.495C5.77917 19.7684 6.22239 19.7684 6.49576 19.495L12.5008 13.49L18.5058 19.495C18.7792 19.7684 19.2224 19.7684 19.4958 19.495C19.7691 19.2216 19.7691 18.7784 19.4958 18.505L13.4907 12.5L19.4958 6.49499Z' fill='%234F5588'/%3E%3C/svg%3E")
    50% 50% no-repeat;
}
</style>
