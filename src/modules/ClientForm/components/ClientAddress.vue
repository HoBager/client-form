<template>
  <div class="address">
    <h4 class="address__title">{{ "Адрес" }}</h4>
    <div class="address__fields">
      <UInput
        class="address__field"
        v-for="(item, name) in clientAddress"
        :key="item.key"
        v-model="clientAddress[name]"
        :label="fieldNames[name]"
        :error="v$.clientAddress[name]?.$errors"
      />
    </div>
  </div>
</template>

<script>
import UInput from "@/ui/UInput.vue";
import { useVuelidate } from "@vuelidate/core";
import { required, helpers } from "@vuelidate/validators";
export default {
  setup() {
    return { v$: useVuelidate() };
  },
  components: { UInput },
  props: ["value"],
  data() {
    return {
      clientAddress: {
        index: "",
        country: "",
        region: "",
        city: "",
        street: "",
        house: "",
      },
      fieldNames: {
        index: "Индекс",
        country: "Страна",
        region: "Область",
        city: "Город",
        street: "Улица",
        house: "Дом",
      },
    };
  },
  watch: {
    clientAddress: {
      handler: function () {
        this.$emit("input", this.clientAddress);
      },
      deep: true,
    },
  },
  validations() {
    return {
      clientAddress: {
        city: {
          required: helpers.withMessage("Должно быть заполненно", required),
        },
      },
    };
  },
};
</script>

<style lang="scss" scoped>
.address {
  &__title {
    margin-bottom: 16px;
  }

  &__fields {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 8px;
  }
  &__field {
    width: 32%;
  }
}

@media (max-width: 576px) {
  .address {
    &__fields {
      gap: 4px;
    }
    &__field {
      width: 49%;
    }
  }
}
</style>
