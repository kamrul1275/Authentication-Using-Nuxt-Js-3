<template>
  <br />
  <br />
  <br />
  <br />
  <h2>User Login</h2>

  {{ token.getToken }}
  {{ token.getStatus }}

  <form class="max-w-sm mx-auto" @click.prevent="handleSubmite()">
    <div class="mb-5">
      <label
        for="email"
        class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
        >email</label
      >
      <input
        type="email"
        v-model="user.email"
        id="email"
        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        placeholder="name@flowbite.com"
        required
      />
      <span v-if="errors.email" class="text-red-500">{{ errors.email[0] }}</span>
    </div>

    <div class="mb-5">
      <label
        for="password"
        class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
        >password</label
      >
      <input
        type="password"
        v-model="user.password"
        id="password"
        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        required
      />
      <span v-if="errors.password" class="text-red-500">{{ errors.password[0] }}</span>
    </div>

    <button
      type="submit"
      class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
    >
      Submit
    </button>
  </form>
</template>

<script setup>
definePageMeta({
  middleware: ["guest"],
  // or middleware: 'auth'
});

const auth = useAuthStore();
const token = useTokenStore();
const user = reactive({
  email: "",
  password: "",
});

const errors = ref([]);

const handleSubmite = async () => {
  try {
    await auth.login(user);

    //console.log(auth.login);
  } catch (error) {
    errors.value = error.data.errors;
  }
};
</script>

<style lang="scss" scoped></style>
