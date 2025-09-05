<template>
  <q-page class="register-page">
    <q-container class="q-pa-md">
      <q-card class="q-ma-auto">
        <q-card-section>
          <div class="text-center text-h6">Kayıt Ol</div>
        </q-card-section>

        <q-form @submit="register">
          <q-input v-model="email" type="email" placeholder="E-posta" filled />
          <q-input v-model="password" type="password" placeholder="Şifre" filled />

          <q-btn type="submit" label="Kayıt Ol" color="primary" class="full-width q-mt-md" />
        </q-form>
      </q-card>
    </q-container>
  </q-page>
</template>

<script>
import { createUserWithEmailAndPassword } from 'firebase/auth';
import { auth } from '../firebase';

export default {
  data() {
    return {
      email: '',
      password: ''
    };
  },
  methods: {
    async register() {
      try {
        const userCredential = await createUserWithEmailAndPassword(
          auth,
          this.email,
          this.password
        );
        console.log('Kayıt başarılı:', userCredential.user);
        this.$router.push('/login');
      } catch (error) {
        console.error('Kayıt hatası:', error);
        alert(`Kayıt sırasında hata oluştu: ${error.code}`);
      }
    }
  }
};
</script>

