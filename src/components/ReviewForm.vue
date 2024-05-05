<template>
  <div>
    <h2>Step: review</h2>
    <p>Review your details:</p>
    <p>
      Username: <span>{{ userData.username }}</span>
    </p>
    <p>
      Email: <span>{{ userData.email }}</span>
    </p>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  userData: Object,
});
</script>
