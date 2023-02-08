<template>
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
const { auth } = useSupabaseClient();
const router = useRouter();
const user = useSupabaseUser();
const isSignUp = ref(false);

const email = ref('');
const password = ref('');

const signUp = async () => {
  const { error } = await auth.signUp({
    email: email.value,
    password: password.value,
  });
  if (error) {
    alert('check your email for email confirmation');
    return;
  }
};

const signIn = async () => {
  console.log('running signIn method!!');
  const { error } = await auth.signInWithPassword({
    email: email.value,
    password: password.value,
  });
  if (error) console.log(error.message);
};

watchEffect(async () => {
  if (user.value) {
    console.log(user.value);
    return navigateTo('/');
  }
});
</script>
