<script setup lang="ts">
const { clear, user } = useUserSession();
const signOut = () => {
  clear();
  navigateTo("/auth/signin");
};
const items = computed(() => [
  [
    {
      label: user.value?.name,
      avatar: {
        src: user.value?.avatar,
      },
      type: "label",
    },
  ],
  [
    {
      label: "Logout",
      icon: "i-lucide-log-out",
      onSelect: signOut,
    },
  ],
]);
</script>

<template>
  <div v-if="user" class="relative">
    <UDropdownMenu
      :items="items"
      :ui="{
        content: 'w-48',
      }"
    >
      <UAvatar
        v-if="user?.provider === 'github'"
        :src="user?.avatar"
        :alt="user?.name"
        size="xl"
        class="border border-neutral-200 dark:border-neutral-700"
      />
      <UButton v-else icon="lucide:user" variant="text" size="xl" />
    </UDropdownMenu>
  </div>
</template>
