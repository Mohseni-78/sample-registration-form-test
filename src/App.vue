<template>
  <div>
    <h2 v-if="step === 1">Step: username</h2>
    <h2 v-if="step === 2">Step: email</h2>
    <h2 v-if="step === 3">Step: review</h2>

    <input
      v-if="step === 1"
      type="text"
      id="username"
      name="username"
      placeholder="Username"
      v-model="username"
      @input="validateUsername"
    />

    <input
      v-if="step === 2"
      type="text"
      id="email"
      name="email"
      placeholder="Email"
      v-model="email"
      @input="validateEmail"
    />

    <div v-if="step === 3">
      <p>Review your details:</p>
      <p>Username: {{ username }}</p>
      <p>Email: {{ email }}</p>
    </div>

    <button :disabled="step === 1" id="btn-prev" @click="prevStep">Prev</button>
    <button :disabled="step === 3 || !isValid" id="btn-next" @click="nextStep">Next</button>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

const step = ref(1);
const username = ref("");
const email = ref("");
const isValid = ref(false);

const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

const validateUsername = () => {
  isValid.value = !!username.value; // Example validation
};

const validateEmail = () => {
  isValid.value = emailPattern.test(email.value);
};

watch(email, validateEmail);

const nextStep = () => {
  if (step.value < 3 && isValid.value) {
    step.value++;
  }
};

const prevStep = () => {
  if (step.value > 1) {
    step.value--;
  }
};
</script>
