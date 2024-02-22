<script setup>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import PaymentView from "@/Views/PaymentView.vue";
import Error from "@/components/Error.vue";
import state from "@/state";
import { ref } from "vue";

// const error = ref("");

// const setError = (msg) => {
//   error.value = msg;
// };
</script>

<template>
  <Header />
  <Error :msg="state.error"></Error>
  <PaymentView @onError="setError"></PaymentView>
  <Footer />
</template>
