<template>
  <div>
    <NuxtPage />

    <!-- Bottom Navigation Component -->
    <div class="fixed">
      <BottomNavigation @nav-change="handleNavChange" />
    </div>
  </div>
</template>
<script setup lang="ts">
const handleNavChange = (index: number) => {
  console.log("App.vue: Navigation changed to index:", index);
  try {
    if (index === 0) {
      // Navigate to home page
      console.log("App.vue: Navigating to home page");
      navigateTo("/");
    } else if (index === 1) {
      // Navigate to wallet page
      console.log("App.vue: Navigating to wallet page");
      navigateTo("/wallet");
    } else if (index === 2) {
      // Navigate to profile page
      console.log("App.vue: Navigating to profile page");
      navigateTo("/profile");
    }
  } catch (error) {
    console.error("App.vue: Navigation error:", error);
  }
};
</script>
