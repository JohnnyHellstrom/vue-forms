<template>
  <div class="bg-red-700 text-white p-2 w-full my-2" v-if="msg">{{ msg }}</div>
</template>

<script setup>
defineProps({
  msg: String,
});
</script>
