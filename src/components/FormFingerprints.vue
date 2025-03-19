<script setup>
defineProps({
  Data: Object,
  language: String,
});
</script>

<template>
  <main class="form_group">
    <div
      v-for="(fingerprint, index) in Data.online_fingerprints"
      :key="index"
      class="form_data"
    >
      <label>
        {{ language === "ar" ? "البصمات الرقمية" : "Online Fingerprints" }}
      </label>
      <input type="text" v-model="fingerprint.name" required />
    </div>
    <div
      v-for="(fingerprint, index) in Data.online_fingerprints"
      :key="index"
      class="form_data"
    >
      <label for="name">
        {{ language === "ar" ? "العنواني الاسم" : "Name Address" }}
      </label>
      <input type="text" v-model="fingerprint.description" required />
    </div>
    <div
      v-for="(fingerprint, index) in Data.online_fingerprints"
      :key="index"
      class="form_data"
    >
      <label for="description">
        {{ language === "ar" ? "الرابط" : "URl" }}
      </label>
      <input type="url" v-model="fingerprint.url" required />
    </div>
  </main>
</template>

<style scoped>
</style>