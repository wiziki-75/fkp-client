<template>
  <div class="home">
    <h1>Bienvenue sur notre site de cours en ligne !</h1>
    <p>Explorez nos cours gratuits et commencez à apprendre dès aujourd'hui.</p>
    <router-link to="/register" class="btn-register">S'inscrire</router-link><br>

    <!-- Afficher les cours -->
    <br><div class="courses">
      <div v-for="course in courses" :key="course.id">
        <!-- Utilisation d'un lien pour chaque cours -->
        <a :href="'/course/' + course.id">
          <h2>{{ course.course_name }}</h2>
          <p>{{ course.description }}</p>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'HomePage',
  data() {
    return {
      courses: [], // Tableau pour stocker les cours
    };
  },
  mounted() {
    // Effectuer une requête GET à l'API
    axios
      .get('http://localhost:3000/courses')
      .then((response) => {
        // Stocker les données de la réponse dans le tableau courses
        this.courses = response.data;
      })
      .catch((error) => {
        console.error('Erreur lors de la récupération des cours :', error);
      });
  },
};
</script>

<style scoped lang="css" src="./HomePage.css"></style>
