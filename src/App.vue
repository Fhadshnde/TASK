<script setup>
import axios from "axios";
import { onMounted, reactive, ref } from "vue";
import FormInputs from "./components/FormInputs.vue";
import FormRoomOptions from "./components/FormRoomOptions.vue";
import FormClientServices from "./components/FormClientServices.vue";
import FormCulturalPayments from "./components/FormCulturalPayments.vue";
import FormCapacity from "./components/FormCapacity.vue";
import FormLocation from "./components/FormLocation.vue";
import FormFingerprints from "./components/FormFingerprints.vue";
import FormOperationalDetails from "./components/FormOperationalDetails.vue";
import FormSubmit from "./components/FormSubmit.vue";

const Options = reactive({
  mainCategories: [] || null,
  categories: [] || null,
  acceptedPayments: [] || null,
  clientTypes: [] || null,
  competitiveAdvantages: [] || null,
  culturalShows: [] || null,
  extraServices: [] || null,
  languageSupports: [] || null,
  paymentCategories: [] || null,
  reservationTypes: [] || null,
  roomEquipments: [] || null,
  roomOptions: [] || null,
});

const Data = reactive({
  name: "",
  email: "",
  phone_number: null,
  country_code: "+964",
  main_categories: null,
  categories: null,
  category: null,
  accepted_payments: null,
  client_types: null,
  competitive_advantages: null,
  cultural_shows: null,
  extra_services: null,
  language_supports: null,
  payment_categories: null,
  reservation_types: null,
  room_equipments: null,
  room_options: null,
  social_media_accounts: {
    website: "",
    facebook: "",
    instagram: "",
    youtube: "",
    tiktok: "",
    snapchat: "",
  },
  capacity_and_capabilities: {
    number_of_rooms: null,
    number_of_seats: null,
    number_of_guests: null,
  },
  location: {
    country: "",
    city: "",
    district: "",
    street: "",
    google_map_url: "",
    nearest_landmark: "",
    longitude: null,
    latitude: null,
  },
  online_fingerprints: [
    {
      name: "",
      description: "",
      url: "",
    },
  ],
  operational_details: {
    is_always_open: false,
    reservation_types: [],
    working_hour: [
      {
        day_of_week: 0,
        start_time: "",
        end_time: "",
      },
    ],
    seasonal_working_hour_change: "",
    cancellation_policy: "",
  },
});

const fetchOptions = async () => {
  try {
    const response = await axios.get(
      "https://simpleapplicablesolutions.pythonanywhere.com/tourist/guide/api/tourist/facility/form-data/"
    );

    Options.categories = response.data.categories;
    Options.mainCategories = response.data.main_categories;
    Options.acceptedPayments = response.data.accepted_payments;
    Options.clientTypes = response.data.client_types;
    Options.competitiveAdvantages = response.data.competitive_advantages;
    Options.culturalShows = response.data.cultural_shows;
    Options.extraServices = response.data.extra_services;
    Options.languageSupports = response.data.language_supports;
    Options.paymentCategories = response.data.payment_categories;
    Options.reservationTypes = response.data.reservation_types;
    Options.roomEquipments = response.data.room_equipments;
    Options.roomOptions = response.data.room_options;
  } catch (error) {
    console.error(error);
  }
};

// عند تحميل الصفحة
onMounted(() => {
  fetchOptions();
  const savedLanguage = localStorage.getItem("language") || "en";
  if (savedLanguage) {
    language.value = savedLanguage;
  }
});

const phoneError = ref("");
const validatePhoneNumber = () => {
  let fullPhoneNumber = `${Data.country_code}${Data.phone_number.replace(/\D/g, "")}`;
  const iraqPhoneRegex = /^\+964\d{10}$/;
  if (!iraqPhoneRegex.test(fullPhoneNumber)) {
    phoneError.value =
      language.value === "en"
        ? "Phone number must start with +964 and be 10 digits long."
        : "يجب أن يبدأ الرقم بـ +964 ويتكون من 10 أرقام.";
  } else {
    phoneError.value = "";
  }
};

const submitForm = async () => {
  try {
    validatePhoneNumber();
    if (phoneError.value) {
      alert(phoneError.value);
      return;
    }
    const fullPhoneNumber = `${Data.country_code}${Data.phone_number.replace(/\D/g, "")}`;

    await axios.post(
      "https://simpleapplicablesolutions.pythonanywhere.com/tourist/guide/api/tourist/facility/p1/",
      { ...Data, phone_number: fullPhoneNumber }
    );

    alert(language.value === "en" ? "The request has been sent." : "تم إرسال الطلب.");
  } catch (error) {
    console.error(error);
  }
};

const language = ref("en");
const toggleLanguage = () => {
  language.value = language.value === "en" ? "ar" : "en";
  localStorage.setItem("language", language.value);
};
</script>

<template>
  <section class="container" :dir="language === 'ar' ? 'rtl' : 'ltr'">
    <button class="lang_toggle" @click="toggleLanguage">
      {{ language === "en" ? "Ar" : "En" }}
    </button>
    <h2 class="form_title">
      {{ language === "ar" ? "قم بتسجيل المعملومات" : "Record the information" }}
    </h2>
    <form @submit.prevent="submitForm" class="signup_form">
      <FormInputs :Data="Data" :language="language" :phoneError="phoneError" @validatePhoneNumber="validatePhoneNumber" />
      <FormRoomOptions :Data="Data" :Options="Options" :language="language" />
      <FormClientServices :Data="Data" :Options="Options" :language="language" />
      <FormCulturalPayments :Data="Data" :Options="Options" :language="language" />
      <FormCapacity :Data="Data" :language="language" />
      <FormLocation :Data="Data" :language="language" />
      <FormFingerprints :Data="Data" :language="language" />
      <FormOperationalDetails :Data="Data" :Options="Options" :language="language" />
      <FormSubmit :language="language" />
    </form>
  </section>
</template>

<style>
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f9fafb;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.lang_toggle {
  background-color: #3b82f6;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 14px;
  margin-bottom: 20px;
}

.lang_toggle:hover {
  background-color: #2563eb;
}

.form_title {
  font-size: 24px;
  font-weight: bold;
  color: #1f2937;
  margin-bottom: 20px;
  text-align: center;
}

.signup_form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.form_group {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
}

.form_data {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

label {
  font-size: 14px;
  font-weight: 500;
  color: #374151;
}

input,
select {
  padding: 10px;
  border: 1px solid #d1d5db;
  border-radius: 8px;
  font-size: 14px;
  background-color: white;
  transition: border-color 0.3s ease;
}

input:focus,
select:focus {
  outline: none;
  border-color: #3b82f6;
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

.error {
  color: #ef4444;
  font-size: 12px;
  margin-top: 4px;
}

.Btn {
  background-color: #3b82f6;
  color: white;
  border: none;
  padding: 12px 24px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 16px;
  font-weight: 500;
  transition: background-color 0.3s ease;
}

.Btn:hover {
  background-color: #2563eb;
}

[dir="rtl"] {
  text-align: right;
}

@media (max-width: 700px) {
  .form_group {
    grid-template-columns: 1fr;
  }
}
</style>