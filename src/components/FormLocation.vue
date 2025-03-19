<script setup>
defineProps({
  Data: Object,
  language: String,
});
</script>

<template>
  <main class="form_group">
    <div class="form_data">
      <label for="country">
        {{ language === "ar" ? "الدولة" : "Country" }}
      </label>
      <input type="text" id="country.id" v-model="Data.location.country" required />
    </div>

    <div class="form_data">
      <label for="city">
        {{ language === "ar" ? "المدينة" : "City" }}
      </label>
      <input type="text" id="city" v-model="Data.location.city" required />
    </div>

    <div class="form_data">
      <label for="district">
        {{ language === "ar" ? "الحي" : "District" }}
      </label>
      <input type="text" id="district" v-model="Data.location.district" required />
    </div>
  </main>

  <main class="form_group">
    <div class="form_data">
      <label for="street">
        {{ language === "ar" ? "الشارع" : "Street" }}
      </label>
      <input type="text" id="street" v-model="Data.location.street" required />
    </div>

    <div class="form_data">
      <label for="nearest_landmark">
        {{ language === "ar" ? "أقرب معلم" : "Nearest Landmark" }}
      </label>
      <input
        type="text"
        id="nearest_landmark"
        v-model="Data.location.nearest_landmark"
        required
      />
    </div>

    <div class="form_data">
      <label for="google_map_url">
        {{ language === "ar" ? "رابط خريطة جوجل" : "Google Map URL" }}
      </label>
      <input
        type="url"
        id="google_map_url"
        v-model="Data.location.google_map_url"
        required
      />
    </div>
  </main>
</template>

<style scoped>
</style>