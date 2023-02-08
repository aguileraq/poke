<template>
  <div>Dashboard</div>
</template>

<script setup lang="ts">
const { auth } = useSupabaseClient();
const user = useSupabaseUser();
const router = useRouter();

const logout = async () => await auth.singOut();

definePageMeta({
  middleware: 'auth',
});

watchEffect(async () => {
  if (!user.value) {
    await router.push('/sign');
  }
});
</script>
