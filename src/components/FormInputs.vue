<script setup>
defineProps({
  Data: Object,
  language: String,
  phoneError: String,
});

defineEmits(['validatePhoneNumber']);
</script>

<template>
  <main class="form_inputs">
    <div class="form_data">
      <label for="name">{{ language === "ar" ? "الاسم" : "Name" }}</label>
      <input type="text" id="name" v-model="Data.name" required />
    </div>

    <div class="form_data">
      <label for="email">{{ language === "ar" ? "الايميل" : "Email" }}</label>
      <input type="email" id="email" v-model="Data.email" required />
    </div>

    <div class="form_data">
      <label for="phone">{{ language === "ar" ? "الهاتف" : "Phone" }}</label>
      <div class="phone-container">
        <span class="phone-prefix">+964</span>
        <input
          type="tel"
          id="phone"
          v-model="Data.phone_number"
          @input="$emit('validatePhoneNumber')"
          required
          maxlength="10"
        />
      </div>
      <small v-if="phoneError" class="error">{{ phoneError }}</small>
    </div>

    <div class="form_data">
      <label for="website">{{ language === "ar" ? "الموقع الإلكتروني" : "Website" }}</label>
      <input
        type="url"
        id="website"
        v-model="Data.social_media_accounts.website"
        required
        placeholder="https://example.com"
      />
    </div>
  </main>
</template>

<style scoped>
.phone-container {
  display: flex;
  align-items: center;
  gap: 8px;
}

.phone-prefix {
  background-color: #e5e7eb;
  padding: 10px;
  border-radius: 8px;
  font-size: 14px;
}
</style>