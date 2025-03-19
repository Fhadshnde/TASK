<script setup>
defineProps({
  Data: Object,
  Options: Object,
  language: String,
});
</script>

<template>
  <div class="form_data">
    <label for="category">
      {{ language === "ar" ? "التصنيف" : "Category" }}
    </label>
    <select id="category" v-model="Data.category" required>
      <option value="" disabled selected>
        {{ language === "ar" ? "اختر التصنيف" : "Select a category" }}
      </option>
      <option v-for="cat in Options.categories" :key="cat.id" :value="cat.id">
        {{ cat.name }}
      </option>
    </select>
  </div>

  <div class="form_group">
    <div
      v-for="(hour, index) in Data.operational_details.working_hour"
      :key="index"
      class="form_data"
    >
      <label>
        {{ language === "ar" ? "ساعات العمل" : "Working Hours" }}
      </label>
      <select v-model="hour.day_of_week">
        <option
          v-for="(day, idx) in [
            'Sunday',
            'Monday',
            'Tuesday',
            'Wednesday',
            'Thursday',
            'Friday',
            'Saturday',
          ]"
          :key="idx"
          :value="idx"
        >
          {{ language === "ar" ? `يوم ${day}` : day }}
        </option>
      </select>
      <input type="time" v-model="hour.start_time" required />
      <input type="time" v-model="hour.end_time" required />
    </div>
  </div>

  <div class="form_data">
    <label for="reservation_types">
      {{ language === "ar" ? "أنواع الحجز" : "Reservation Types" }}
    </label>
    <select
      id="reservation_types"
      v-model="Data.operational_details.reservation_types"
      required
    >
      <option
        v-for="type in Options.reservationTypes"
        :key="type.id"
        :value="[type.id]"
      >
        {{ type.name }} - {{ type.description }}
      </option>
    </select>
  </div>

  <div class="form_data">
    <label for="is_always_open">
      {{ language === "ar" ? "هل مفتوح دائمًا؟" : "Is Always Open?" }}
    </label>
    <input
      type="checkbox"
      id="is_always_open"
      v-model="Data.operational_details.is_always_open"
      required
    />
  </div>
</template>

<style scoped>
</style>