<template>
    <div>
        <div v-if="user" @click="logout">Logout</div>
    </div>
</template>

<script setup lang="ts">

const client = useSupabaseAuthClient()
const user = useSupabaseUser()

const logout = async () => {
    await client.auth.signOut()
    navigateTo('/')
}


</script>