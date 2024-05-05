<template>
  <div>
    <h2>Step: email</h2>
    <input
      type="text"
      id="email"
      name="email"
      placeholder="Email"
      v-model="email"
      @input="validateEmail"
      class="mb-4 p-2 border rounded"
    />
  </div>
</template>

<script setup>
import { ref, watch } from "vue";
import { defineEmits } from "vue";

const emits = defineEmits(["update-step"]);

const email = ref("");
const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

const validateEmail = () => {
  const isValid = emailPattern.test(email.value);
  emits("update-step", isValid, { email: email.value });
};

watch(email, validateEmail);
</script>
