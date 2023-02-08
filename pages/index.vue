<template>
  <button type="button" @click="signOut">logout</button>
  <div>Dashboard</div>
</template>

<script setup lang="ts">
const { auth } = useSupabaseClient();
const user = useSupabaseUser();
const router = useRouter();

const logout = async () => await auth.singOut();

watchEffect(async () => {
  if (!user.value) {
    await router.push('/sign');
  }
});

definePageMeta({
  middleware: 'auth',
});
</script>
