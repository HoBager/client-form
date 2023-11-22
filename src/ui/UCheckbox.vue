<template>
  <label class="uicheckbox">
    <input
      @change="$emit('input', $event.target.checked)"
      type="checkbox"
      :value="value"
    />
    {{ label }}
  </label>
</template>

<script>
export default {
  props: ["value", "label"],
};
</script>

<style lang="scss" scoped>
.uicheckbox {
  padding-left: 4px;
}
</style>
