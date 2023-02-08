<template>
  <pre>{{ email }} {{ password }}</pre>
  <form v-if="isSignUp">
    <div>
      <label>Email</label>
      <input type="email" v-model="email" />
    </div>
    <div>
      <label>Password</label>
      <input type="password" v-model="password" />
    </div>
    <div>
      <button type="submit" @click.prevent="signUp">SignUp</button>
    </div>
    <p>
      already have an account?
      <button type="button" @click="isSignUp = !isSignUp">Click here</button>
    </p>
  </form>
  <form v-else>
    <div>
      <label>Email</label>
      <input type="email" v-model="email" />
    </div>
    <div>
      <label>Password</label>
      <input type="password" v-model="password" />
    </div>
    <div>
      <button type="submit" @click.prevent="signIn">signIn</button>
    </div>
    <p>
      Don't have an account?
      <button type="button" @click="isSignUp = !isSignUp">Click here</button>
    </p>
  </form>
</template>

<script setup lang="ts">
const client = useSupabaseClient();
const isSignUp = ref(false);

const email = ref('');
const password = ref('');

const signUp = async () => {
  console.log('signup!!');
  const { user, error } = await client.auth.signUp({
    email: email.value,
    password: password.value,
  });
  console.log(user);
  console.warn(error);
};
const signIn = async () => {
  const { user, error } = await client.auth.signInWithPassword({
    email: email.value,
    password: password.value,
  });
  console.log(user);
  console.warn(error);
};

/* watchEffect(() => {
    if (user.value) navigateTo('/dashboard')
}) */
</script>
