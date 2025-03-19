<script setup>
defineProps({
  language: String,
});
</script>

<template>
  <button type="submit" class="Btn">
    {{ language === "ar" ? "ارسال" : "Submit" }}
  </button>
</template>

<style scoped>
</style>