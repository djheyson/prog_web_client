
<template>
  <user-form :action="'Register'" @form="submit">
    <v-btn text to="/auth">
      Login
    </v-btn>
  </user-form>
</template>

<script>
import UserForm from '@/components/user/Form.vue';

export default {
  name: 'register',
  components: {
    UserForm,
  },
  methods: {
    submit(form) {
      this.$store.dispatch('registerUser', form);
    },
  },
};
</script>

<style scoped></style>
