<template>
  <div class="passport">
    <div class="passport__group group">
      <USelect
        :options="['Паспорт', 'Свидетельство о рождении', 'Вод. удостоверение']"
        v-model="clientPassport.type"
        label="Тип документа"
        class="group__item"
        :error="v$.clientPassport.type.$errors"
      />
      <UDate
        class="group__item date"
        v-model="clientPassport.date"
        label="Дата выдачи"
        :error="v$.clientPassport.date.$errors"
      />
    </div>
    <div class="inputs">
      <UInput
        v-model="clientPassport.series"
        label="Серия"
        class="inputs__item"
      />
      <UInput
        v-model="clientPassport.number"
        label="Номер"
        class="inputs__item"
      />
      <UInput
        v-model="clientPassport.issued"
        label="Кем выдан"
        class="inputs__item inputs__item_big"
      />
    </div>
  </div>
</template>

<script>
import UDate from "@/ui/UDate.vue";
import UInput from "@/ui/UInput.vue";
import USelect from "@/ui/USelect.vue";
import { useVuelidate } from "@vuelidate/core";
import { required, helpers } from "@vuelidate/validators";
export default {
  setup() {
    return { v$: useVuelidate() };
  },
  components: { UDate, UInput, USelect },
  data() {
    return {
      clientPassport: {
        type: "",
        series: "",
        number: "",
        issued: "",
        date: "",
      },
    };
  },
  watch: {
    clientPassport: {
      handler: function () {
        this.$emit("input", this.clientPassport);
      },
      deep: true,
    },
  },
  validations() {
    return {
      clientPassport: {
        date: {
          required: helpers.withMessage("Должно быть заполненно", required),
        },
        type: {
          required: helpers.withMessage("Должно быть заполненно", required),
        },
      },
    };
  },
};
</script>

<style lang="scss" scoped>
.passport {
  .group {
    display: flex;
    gap: 8px;
    &__item {
      width: 49%;
    }
  }
}

.inputs {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 4px;

  &__item {
    width: 20%;

    &_big {
      width: 56%;
    }
  }
}
.date {
  height: 46px;
}

@media (max-width: 576px) {
  .inputs {
    &__item {
      width: 49%;

      &_big {
        width: 100%;
      }
    }
  }
}
</style>
