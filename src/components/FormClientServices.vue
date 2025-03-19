<script setup>
defineProps({
  Data: Object,
  Options: Object,
  language: String,
});
</script>

<template>
  <main class="form_group">
    <div class="form_data">
      <label for="client_types">
        {{ language === "ar" ? "أنواع العملاء" : "Client Types" }}
      </label>
      <select id="client_types" v-model="Data.client_types" required>
        <option
          v-for="client in Options.clientTypes"
          :key="client.id"
          :value="[client.id]"
        >
          {{ client.name }} - {{ client.description }}
        </option>
      </select>
    </div>

    <div class="form_data">
      <label for="extra_services">
        {{ language === "ar" ? "الخدمات الإضافية" : "Extra Services" }}
      </label>
      <select id="extra_services" v-model="Data.extra_services" required>
        <option
          v-for="service in Options.extraServices"
          :key="service.id"
          :value="[service.id]"
        >
          {{ service.name }} - {{ service.description }}
        </option>
      </select>
    </div>

    <div class="form_data">
      <label for="language_supports">
        {{ language === "ar" ? "اللغات المدعومة" : "Supported Languages" }}
      </label>
      <select id="language_supports" v-model="Data.language_supports" required>
        <option
          v-for="lang in Options.languageSupports"
          :key="lang.id"
          :value="[lang.id]"
        >
          {{ lang.name }} - {{ lang.description }}
        </option>
      </select>
    </div>
  </main>
</template>

<style scoped>
</style>