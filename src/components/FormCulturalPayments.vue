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
      <label for="cultural_shows">
        {{ language === "ar" ? "العروض الثقافية" : "Cultural Shows" }}
      </label>
      <select id="cultural_shows" v-model="Data.cultural_shows" required>
        <option
          v-for="show in Options.culturalShows"
          :key="show.id"
          :value="[show.id]"
        >
          {{ show.name }} - {{ show.description }}
        </option>
      </select>
    </div>

    <div class="form_data">
      <label for="payment_categories">
        {{ language === "ar" ? "فئات الدفع" : "Payment Categories" }}
      </label>
      <select id="payment_categories" v-model="Data.payment_categories" required>
        <option
          v-for="payment in Options.paymentCategories"
          :key="payment.id"
          :value="[payment.id]"
        >
          {{ payment.name }} - {{ payment.description }}
        </option>
      </select>
    </div>

    <div class="form_data">
      <label for="accepted_payments">
        {{ language === "ar" ? "طرق الدفع المقبولة" : "Accepted Payments" }}
      </label>
      <select id="accepted_payments" v-model="Data.accepted_payments" required>
        <option
          v-for="payment in Options.acceptedPayments"
          :key="payment.id"
          :value="[payment.id]"
        >
          {{ payment.name }} - {{ payment.description }}
        </option>
      </select>
    </div>
  </main>
</template>

<style scoped>
</style>