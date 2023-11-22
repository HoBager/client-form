<template>
  <div class="client">
    <div class="fullname">
      <u-input
        label="Фамилия"
        class="fullname__field"
        placeholder="Фамилия"
        v-model="clientInfo.firstname"
        :error="v$.clientInfo.firstname.$errors"
      />
      <u-input
        label="Имя"
        class="fullname__field"
        placeholder="Имя"
        v-model="clientInfo.lastname"
        :error="v$.clientInfo.lastname.$errors"
      />
      <u-input
        label="Отчество"
        class="fullname__field"
        placeholder="Отчество"
        v-model="clientInfo.surname"
      />
      <u-date
        label="Дата Рождения"
        class="fullname__field"
        v-model="clientInfo.date"
        :error="v$.clientInfo.date.$errors"
      />
      <phone-input
        label="Номер телефона"
        class="fullname__field"
        v-model="clientInfo.phone"
        :error="v$.clientInfo.phone.$errors"
      />
    </div>

    <div class="selects">
      <multi-select
        class="selects__item"
        :label="'Группа клиентов'"
        v-model="clientInfo.clientGroup"
        :options="['VIP', 'Проблемные', 'ОМС']"
        :error="v$.clientInfo.clientGroup.$errors"
      />
      <u-select
        class="selects__item"
        v-model="clientInfo.doctor"
        :options="['Иванов', 'Захаров', 'Чернышева']"
        label="Лечащий Врач"
      />
    </div>
    <u-checkbox v-model="clientInfo.sms" label="Не отправлять СМС" />
  </div>
</template>

<script>
import UInput from "@/ui/UInput.vue";
import UDate from "@/ui/UDate.vue";
import PhoneInput from "@/components/PhoneInput.vue";
import MultiSelect from "@/components/MultiSelect.vue";
import USelect from "@/ui/USelect.vue";
import UCheckbox from "@/ui/UCheckbox.vue";
import { useVuelidate } from "@vuelidate/core";
import { required, helpers, minLength } from "@vuelidate/validators";
export default {
  setup() {
    return { v$: useVuelidate() };
  },
  components: { UInput, UDate, PhoneInput, MultiSelect, USelect, UCheckbox },
  props: ["value", "stepState"],
  data() {
    return {
      clientInfo: {
        firstname: "",
        lastname: "",
        surname: "",
        phone: "",
        date: "",
        clientGroup: [],
        doctor: "",
        sms: false,
      },
    };
  },
  watch: {
    clientInfo: {
      handler: function () {
        this.$emit("input", this.clientInfo);
      },
      deep: true,
    },
  },
  validations() {
    return {
      clientInfo: {
        firstname: {
          required: helpers.withMessage("Должно быть заполненно", required),
        },
        lastname: {
          required: helpers.withMessage("Должно быть заполненно", required),
        },
        date: {
          required: helpers.withMessage("Должно быть заполненно", required),
        },
        phone: {
          minLength: helpers.withMessage("Не корретный номер", minLength(12)),
          required: helpers.withMessage("Должно быть заполненно", required),
        },
        clientGroup: {
          required: helpers.withMessage("Должно быть заполненно", required),
        },
      },
    };
  },
};
</script>

<style lang="scss" scoped>
.client {
  display: flex;
  flex-direction: column;
  width: 100%;
  gap: 8px;
}
.fullname {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-bottom: 8px;

  &__field {
    width: 32%;
  }
}

.selects {
  display: flex;
  justify-content: space-between;

  &__item {
    width: 49%;
  }
}

@media (max-width: 576px) {
  .fullname {
    gap: 4px;
    &__field {
      width: 49%;
    }
  }
}
</style>
