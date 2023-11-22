<template>
  <form @submit.prevent="handleSubmit" class="client-form">
    <ClientInfo class="client-form__info" v-model="form.clientInfo" />
    <ClientAddress class="client-form__address" v-model="form.clientAddress" />
    <ClientPassport v-model="form.clientPassport" />
    <UButton type="submit" text="Отправить" />
    <AlertMessage v-if="showModal" @close="closeModal" />
  </form>
</template>

<script>
import ClientInfo from "./components/ClientInfo.vue";
import ClientAddress from "./components/ClientAddress.vue";
import ClientPassport from "./components/ClientPassport.vue";
import UButton from "../../ui/UButton.vue";
import AlertMessage from "@/components/AlertMessage.vue";
import { useVuelidate } from "@vuelidate/core";
export default {
  components: {
    ClientInfo,
    ClientAddress,
    ClientPassport,
    UButton,
    AlertMessage,
  },
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      showModal: false,
      form: {
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
        clientAddress: {
          index: "",
          country: "",
          region: "",
          city: "",
          street: "",
          house: "",
        },
        clientPassport: {
          type: "",
          series: "",
          number: "",
          issued: "",
          date: "",
        },
      },
    };
  },
  methods: {
    async handleSubmit() {
      const validate = await this.v$.$validate();
      console.log(validate);
      if (validate) {
        this.showModal = true;
      }
    },
    closeModal() {
      this.showModal = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.client-form {
  display: flex;
  flex-direction: column;
  width: 100%;
  min-height: 500px;
  max-width: 700px;
  border: 1px solid #aaaaaa;
  padding: 12px;
  border-radius: 4px;
  box-shadow: 0 0 5px 1px #aaaaaa;

  &__info,
  &__address {
    margin-bottom: 24px;
  }
}
</style>
