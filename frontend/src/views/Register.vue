<template>
  <div class="min-h-screen bg-green-950 flex items-center justify-center p-4">
    <div class="bg-green-900 border border-green-800 rounded-2xl shadow-2xl p-8 w-full max-w-md">

      <h1 class="text-2xl font-bold text-green-50 text-center mb-7">🎓 Inscription</h1>

      <div v-if="error" class="mb-4 px-4 py-3 rounded-lg bg-red-500/10 border border-red-500/20 text-red-400 text-sm">{{ error }}</div>
      <div v-if="success" class="mb-4 px-4 py-3 rounded-lg bg-green-500/10 border border-green-400/30 text-green-300 text-sm">{{ success }}</div>

      <form @submit.prevent="handleRegister">
        <div class="mb-4">
          <label for="name" class="block text-sm font-medium text-green-300 mb-1.5">Nom complet</label>
          <input type="text" id="name" v-model="fo          <input type="text" id="name" v-model="fo          <input type="text" id="name" v-model="fo          <input type="text" id="name" v-model="fo          <input type="text" id= fo          <ineen-400 focus:ring-2 focus:ring-green-400/20 transition-all text-sm" />
        </div>

        <div class="mb-4">
          <label for="email" class="block text-sm font-medium text-green-300 mb-1.5">Email</label>
          <input type="email" id="email" v-model="form.email" placeholder="jean.dupont@example.com" required
            class="w-full px-4 py-3 bg-green-950 border border-green-700 rounded-lg text-green-50 placeholder-green-700 focus:outline-none focus:border-green-400 focus:ring-2 focus:ring-green-400/20 transition-all text-sm" />
        </div>

        <div class="mb-5">
          <label for="password" class="block text-sm font-medium text-green-300 mb-1.5">Mot de passe</label>
          <input type="password" id="password" v-model="form.password" placeholder="Min 6 caractères" required minlength="6"
            class="w-full px-4 py-3 bg-green-950 border border-green-700 rounded-lg text-green-50 placeholder-green-700 focus:outline-none focus:border-green-400 focus:ring-2 focus:ring-green-400/20 transition-all text-sm" />
        </div>

        <button type="submit" :disabled="loading"
          class="w-full py-3 bg-green-600 hover:bg-green-500 disabled:opacity-50 disabled:cursor-not-allowed text-white font-semibold rounded-lg transition-all hover:shadow-lg hover:shadow-green-500/30 cursor-pointer border-none text-sm">
          {{ loading ? 'Inscription...' : "S'inscrire" }}
        </button>
      </form>

      <div class="text-center mt-5 text-sm text-green-600">
        Déjà un compte ? <router-link to="/login" class="text-green-400 hover:text-green-300 font-semibold">Se connecter</router-link>
      </div>

      <div class="mt-6 p-4 rounded-xl bg-green-950/80 border border-green-700/40">
        <h3 class="text-green-400 font-semibold text-sm mb-2">💡 JWT Demo</h3>
        <p class="text-green-600 text-xs leading-relaxed">
          ✅ Pas de session serveur<br>
          ✅ Token stocké dans <code class="bg-green-950 px-1 rounded border border-green-700 text-green-400">localStorage</code><br>
          ✅ MongoDB pour les utilisateurs uniquement
        </p>
      </div>

    </div>
  </div>
</template>

<script>
import { authService } from '../services/api'

export default {
  name: 'Register',
  data() {
    return {
      form: { name: '', email: '', password: '' },
      error: null, success: null, loading: false
    }
  },
  methods: {
    async handleRegister() {
      this.error = null; this.success = null; this.loading = true
      try {
        const response = await authService.register(this.form)
        this.success = response.message
        setTimeout(() => { this.$router.push('/home') }, 1000)
      } catch (err) {
        this.error = err.response?.data?.message || "Erreur lors de l'inscription"
      } finally { this.loading = false }
    }
  }
}
</script>
