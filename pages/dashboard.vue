<template>
  <div>Dashboard</div>
</template>

<script setup lang="ts">
const user = useSupabaseUser();
const router = useRouter();

definePageMeta({
  middleware: 'auth',
});

watchEffect(async () => {
  if (!user.value) {
    await router.push('/login');
  }
});
</script>
