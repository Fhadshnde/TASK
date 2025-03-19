<script setup>
defineProps({
  Data: Object,
  language: String,
});
</script>

<template>
  <main class="form_group">
    <div class="form_data">
      <label for="number_of_rooms">
        {{ language === "ar" ? "عدد الغرف" : "Number of Rooms" }}
      </label>
      <input
        type="number"
        id="number_of_rooms"
        v-model.number="Data.capacity_and_capabilities.number_of_rooms"
        required
      />
    </div>

    <div class="form_data">
      <label for="number_of_seats">
        {{ language === "ar" ? "عدد المقاعد" : "Number of Seats" }}
      </label>
      <input
        type="number"
        id="number_of_seats"
        v-model.number="Data.capacity_and_capabilities.number_of_seats"
        required
      />
    </div>

    <div class="form_data">
      <label for="number_of_guests">
        {{ language === "ar" ? "عدد الضيوف" : "Number of Guests" }}
      </label>
      <input
        type="number"
        id="number_of_guests"
        v-model.number="Data.capacity_and_capabilities.number_of_guests"
        required
      />
    </div>
  </main>
</template>

<style scoped>
</style>