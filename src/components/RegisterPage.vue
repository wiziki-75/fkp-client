<template>
  <div class="register-page">
    <h1 class="page-title">Inscription</h1>
    <form @submit.prevent="register" class="register-form">
      <div class="form-group">
        <label for="username">Nom d'utilisateur</label>
        <input type="text" id="username" v-model="username" required>
      </div>
      <div class="form-group">
        <label for="email">Adresse e-mail</label>
        <input type="email" id="email" v-model="email" required>
      </div>
      <div class="form-group">
        <label for="password">Mot de passe</label>
        <input type="password" id="password" v-model="password" required>
      </div>
      <button type="submit" class="btn-register">S'inscrire</button>
    </form>
    <router-link to="/" class="btn-back">Retour à la page d'accueil</router-link>
    
    <!-- Affichage du message d'erreur -->
    <div v-if="errorMessage" class="error-message">{{ errorMessage }}</div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'RegisterPage',
  data() {
    return {
      username: '',
      email: '',
      password: '',
      errorMessage: '', // Ajout de la propriété errorMessage
    };
  },
  methods: {
    async register() {
      try {
        const response = await axios.post('http://localhost:3000/register', {
          username: this.username,
          email: this.email,
          password: this.password
        });

        if (response.status === 201) {
          console.log('Inscription réussie');
          alert("Inscription réussi.")
          this.$router.push('/');
          // Vous pouvez rediriger l'utilisateur vers une page de confirmation ou de connexion ici
        }
      } catch (error) {
        console.error('Erreur lors de l\'inscription', error);
        if (error.response && error.response.status === 400) {
          // Gérez l'erreur d'e-mail déjà utilisé ici
          this.errorMessage = 'Cet e-mail est déjà utilisé.';
        } else {
          // Gérez d'autres erreurs d'inscription ici
          this.errorMessage = 'Erreur lors de l\'inscription. Veuillez réessayer.';
        }
      }
    }
  }
}
</script>

<style scoped lang="css" src="./RegisterPage.css"></style>
