<template>
  <div class="flex flex-col items-center justify-center p-6">
    <KeepAlive>
      <component :is="currentComponent" @update-step="updateStep" :userData="userData" />
    </KeepAlive>

    <div class="flex space-x-2 mt-4">
      <button
        :disabled="step === 1"
        id="btn-prev"
        @click="prevStep"
        class="px-4 py-2 bg-gray-200 text-gray-800 rounded hover:bg-gray-300 disabled:opacity-50"
      >
        Prev
      </button>
      <button
        :disabled="step === 3 || !isValid"
        id="btn-next"
        @click="nextStep"
        class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600 disabled:opacity-50"
      >
        Next
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import UsernameForm from "./components/UsernameForm.vue";
import EmailForm from "./components/EmailForm.vue";
import ReviewForm from "./components/ReviewForm.vue";

const step = ref(1);
const userData = ref({ username: "", email: "" });
const isValid = ref(false);

const components = {
  1: UsernameForm,
  2: EmailForm,
  3: ReviewForm,
};

const currentComponent = computed(() => components[step.value]);

const updateStep = (valid, data) => {
  isValid.value = valid;
  Object.assign(userData.value, data);
};

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
