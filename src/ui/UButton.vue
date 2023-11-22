<template>
  <button class="uibutton">{{ text }}</button>
</template>

<script>
export default {
  props: ["text"],
};
</script>

<style lang="scss" scoped>
.uibutton {
  background-color: #ee8142;
  max-width: 200px;
  padding: 12px;
  color: #ffffff;
  font-weight: bold;
  font-family: inherit;
  font-size: 1rem;
  box-shadow: 0 0 3px 1px #aaaaaa;

  &:hover {
    background-color: #ef8c53;
  }
}
</style>
