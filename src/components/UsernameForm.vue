<template>
  <div>
    <h2>Step: username</h2>
    <input
      type="text"
      id="username"
      name="username"
      placeholder="Username"
      v-model="username"
      @input="validateUsername"
      class="mb-4 p-2 border rounded"
    />
  </div>
</template>

<script setup>
import { ref, watch } from "vue";
import { defineEmits } from "vue";

const emits = defineEmits(["update-step"]);

const username = ref("");

const validateUsername = () => {
  const isValid = !!username.value; // Example validation
  emits("update-step", isValid, { username: username.value });
};

watch(username, validateUsername);
</script>
