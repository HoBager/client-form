<template>
  <div class="page">
    <client-form />
  </div>
</template>

<script>
import ClientForm from "./modules/ClientForm/ClientForm.vue";
export default {
  components: { ClientForm },
  data: () => ({
    num: 0,
    date: "",
  }),
  watch: {
    date: function (newDate, oldDate) {
      console.log(newDate, oldDate);
    },
  },
};
</script>

<style lang="scss" scoped>
.page {
  display: flex;
  width: 100vw;
  height: 100vh;
  justify-content: center;
  align-items: center;
}

@media (max-width: 576px) {
  .page {
    height: auto;
  }
}
</style>
