<template>
  <div class="container bg-slate-300 mx-auto p-2">
    <h2>Payment</h2>
    <div>
      <form novalidate @submit.prevent="onSubmit()">
        <div class="grid grid-cols-2 gap-2">
          <div>
            <AddressView :model="state.shipping"> <h3 class="mb-6">Shipping Adress</h3></AddressView>
          </div>
          <div>
            <AddressView :model="state.billing" :isDisabled="state.billing.sameAsShipping">
              <h3>Billing</h3>
              <label class="flex">
                <input type="checkbox" v-model="state.billing.sameAsShipping" />
                &nbsp;Same as Shipping?
              </label>
            </AddressView>
          </div>
        </div>
        <div class="w-1/2">
          <h3>Credit Card</h3>
          <label for="cardNumber">Card Number</label>
          <input type="text" id="cardNumber" v-model="state.creditCard.cardNumber" />
          <label for="cardHolder">Name of Card</label>
          <input type="text" id="cardHolder" v-model="state.creditCard.cardHolder" />
          <div class="grid grid-cols-3 gap-2">
            <div>
              <label for="exMonth">Expiration Month</label>
              <select id="exMonth" v-model="state.creditCard.exMonth">
                <option v-for="month in months" :value="month.number">{{ month.name }}</option>
              </select>
            </div>
            <div>
              <label for="exYear">Expiration Year</label>
              <select id="exYear" v-model="state.creditCard.exYear">
                <option v-for="year in years">{{ year }}</option>
              </select>
            </div>
            <div><label for="cvc">CVC</label> <input type="text" id="cvc" v-model="state.creditCard.cvc" /></div>
          </div>
        </div>
        <button type="submit">Next</button>
      </form>
    </div>
    <div>
      <pre>{{ state }}</pre>
    </div>
  </div>
</template>

<script setup>
import months from "@/lookup/months";
import { ref, watch } from "vue";
import AddressView from "@/Views/AddressView.vue";
import state from "@/state";

const emits = defineEmits(["onError"]);

const years = Array.from({ length: 10 }, (_, i) => i + 2023);

const onSubmit = () => {
  state.error = ("onError", "Cant save yet, no API");
};

watch(
  () => state.billing.sameAsShipping,
  () => {
    if (state.billing.sameAsShipping) {
      state.billing.fullName = state.shipping.fullName;
      state.billing.company = state.shipping.company;
      state.billing.address.adress1 = state.shipping.address.adress1;
      state.billing.address.adress2 = state.shipping.address.adress2;
      state.billing.address.cityTown = state.shipping.address.cityTown;
      state.billing.address.stateProvince = state.shipping.address.stateProvince;
      state.billing.address.postalCode = state.shipping.address.postalCode;
    }
  }
);
</script>
