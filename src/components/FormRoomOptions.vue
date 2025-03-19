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
      <label for="room_options">
        {{ language === "ar" ? "خيارات الغرف" : "Room Options" }}
      </label>
      <select id="room_options" v-model="Data.room_options" required>
        <option
          v-for="option in Options.roomOptions"
          :key="option.id"
          :value="[option.id]"
        >
          {{ option.name }} - {{ option.description }}
        </option>
      </select>
    </div>

    <div class="form_data">
      <label for="room_equipments">
        {{ language === "ar" ? "معدات الغرفة" : "Room Equipments" }}
      </label>
      <select id="room_equipments" v-model="Data.room_equipments" required>
        <option
          v-for="equipment in Options.roomEquipments"
          :key="equipment.id"
          :value="[equipment.id]"
        >
          {{ equipment.name }} - {{ equipment.description }}
        </option>
      </select>
    </div>

    <div class="form_data">
      <label for="competitive_advantages">
        {{ language === "ar" ? "المزايا التنافسية" : "Competitive Advantages" }}
      </label>
      <select
        id="competitive_advantages"
        v-model="Data.competitive_advantages"
        required
      >
        <option
          v-for="advantage in Options.competitiveAdvantages"
          :key="advantage.id"
          :value="[advantage.id]"
        >
          {{ advantage.name }} - {{ advantage.description }}
        </option>
      </select>
    </div>
  </main>
</template>

<style scoped>
</style>