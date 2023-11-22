<template>
  <div class="message">
    <div class="message__body">
      <h4>{{ "Отправка Успешна" }}</h4>
      <UButton
        @click.native="$emit('close')"
        type="button"
        class="close"
        text="Закрыть"
      />
    </div>
  </div>
</template>

<script>
import UButton from "@/ui/UButton.vue";
export default { components: { UButton } };
</script>

<style lang="scss" scoped>
.message {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0 8px;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.078);
  z-index: 999;

  &__body {
    display: flex;
    flex-direction: column;

    justify-content: space-around;
    align-items: center;
    max-width: 300px;
    width: 100%;
    height: 200px;
    border: 1px solid #aaaaaa;
    border-radius: 8px;
    background-color: #ffffff;
    box-shadow: 0 0 10px 1px #aaaaaa;
    padding: 12px;

    & .close {
      background-color: rgb(8, 224, 8);
    }
  }
}
</style>
