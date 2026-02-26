<template>
  <div class="min-h-screen bg-lime-50 flex items-center justify-center p-4">
    <div class="bg-white border border-lime-200 rounded-2xl shadow-xl p-8 w-full max-w-md">

      <h1 class="text-2xl font-bold text-slate-900 text-center mb-7">Inscription</h1>

      <div v-if="error" class="mb-4 px-4 py-3 rounded-lg bg-red-50 border border-red-200 text-red-700 text-sm">{{ error }}</div>
      <div v-if="success" class="mb-4 px-4 py-3 rounded-lg bg-lime-100 border border-lime-300 text-lime-900 text-sm">{{ success }}</div>

      <form @submit.prevent="handleRegister">
        <div class="mb-4">
          <label for="name" class="block text-sm font-medium text-slate-800 mb-1.5">Nom complet</label>
          <input type="text" id="name" v-model="form.name" placeholder="Jean Dupont" required
            class="w-full px-4 py-3 bg-white border border-lime-300 rounded-lg text-slate-900 placeholder-slate-500 focus:outline-none focus:border-lime-500 focus:ring-2 focus:ring-lime-500/25 transition-all text-sm" />
        </div>

        <div class="mb-4">
          <label for="email" class="block text-sm font-medium text-slate-800 mb-1.5">Email</label>
          <input type="email" id="email" v-model="form.email" placeholder="jean.dupont@exemple.fr" required
            class="w-full px-4 py-3 bg-white border border-lime-300 rounded-lg text-slate-900 placeholder-slate-500 focus:outline-none focus:border-lime-500 focus:ring-2 focus:ring-lime-500/25 transition-all text-sm" />
        </div>

        <div class="mb-5">
          <label for="password" class="block text-sm font-medium text-slate-800 mb-1.5">Mot de passe</label>
          <input type="password" id="password" v-model="form.password" placeholder="•••••••• (min. 6 caractères)" required minlength="6"
            class="w-full px-4 py-3 bg-white border border-lime-300 rounded-lg text-slate-900 placeholder-slate-500 focus:outline-none focus:border-lime-500 focus:ring-2 focus:ring-lime-500/25 transition-all text-sm" />
        </div>

        <button type="submit" :disabled="loading"
          class="w-full py-3 bg-lime-600 hover:bg-lime-700 disabled:opacity-50 disabled:cursor-not-allowed text-white font-semibold rounded-lg transition-all hover:shadow-lg hover:shadow-lime-600/30 cursor-pointer border-none text-sm">
          {{ loading ? 'Inscription...' : "S'inscrire" }}
        </button>
      </form>

      <div class="text-center mt-5 text-sm text-slate-700">
        Déjà un compte ? <router-link to="/login" class="text-lime-700 hover:text-lime-900 font-semibold">Se connecter</router-link>
      </div>

      <div class="mt-6 p-4 rounded-xl bg-lime-50 border border-lime-300/40">
        <h3 class="text-slate-800 font-semibold text-sm mb-2">JWT Demo</h3>
        <ul class="text-slate-700 text-xs leading-relaxed space-y-1 list-disc list-inside">
          <li>Pas de session serveur</li>
          <li>Token stocké dans <code class="bg-lime-50 px-1 rounded border border-lime-300 text-slate-700">localStorage</code></li>
          <li>MongoDB utilisé pour les utilisateurs</li>
        </ul>
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
