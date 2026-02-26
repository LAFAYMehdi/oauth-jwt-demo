<template>
  <div class="min-h-screen bg-green-950 flex items-center justify-center p-4">
    <div class="bg-green-900 border border-green-800 rounded-2xl shadow-2xl p-8 w-full max-w-md">

      <h1 class="text-2xl font-bold text-green-50 text-center mb-7">🔐 Connexion</h1>

      <div v-if="error" class="mb-4 px-4 py-3 rounded-lg bg-red-500/10 border border-red-500/20 text-red-400 text-sm">{{ error }}</div>
      <div v-if="success" class="mb-4 px-4 py-3 rounded-lg bg-green-500/10 border border-green-400/30 text-green-300 text-sm">{{ success }}</div>

      <form @submit.prevent="handleLogin">
        <div class="mb-4">
          <l          <l          <l          <l          <l          <l          <l          <el>           <          <l          <l          <l          <l          <l          <l          <l          <el>           <          <l          <l          <l          <l          <l          <l          <l          <el>           <          <l     d-l          en-50 placeholder-green-700 focus:outline-none focus:border-green-400 focus:ring-2 focus:ring-green-400/20 transition-all text-sm"
          />
        </div>

        <div class="mb-5">
          <label for="password" class="block text-sm font-medium text-green-300 mb-1.5">Mot de passe</label>
          <input
            type="password"
            id="password"
            v-model="form.password"
            placeholder="Votre mot de passe"
            required
            class="w-full px-4 py-3 bg-green-950 border border-green-700 rounded-lg text-green-50 placeholder-green-700 focus:outline-none focus:border-green-400 focus:ring-2 focus:ring-green-400/20 transition-all text-sm"
          />
        </div>

        <button type="submit" :disabled="loading"
          class="w-full py-3 bg-green-600 hover:bg-green-500 disabled:opacity-50 disabled:cursor-not-allowed text-white font-semibold rounded-lg transition-all hover:shadow-lg hover:shadow-green-500/30 cursor-pointer border-none text-sm">
          {{ loading ? 'Connexion...' : 'Se connecter' }}
        </button>
      </form>

      <div class="text-center mt-5 text-sm text-green-600">
        Pas encore de compte ? <router-link to="/register" class="text-green-400 hover:text-green-300 font-semibold">S'inscrire</router-link>
      </div>

      <div class="flex items-center my-6 text-green-700">
        <div class="flex-1 border-t border-green-800"></div>
        <span class="px-4 text-xs uppercase tracking-wider font-medium">OU</span>
        <div class="flex-1 border-t border-green-800"></div>
      </div>

      <div class="flex flex-col gap-3">
        <button @click="signInWithGoogle" type="button"
          class="w-full flex items-center justify-center gap-3 px-4 py-3 bg-white hover:bg-gray-50 text-gray-700 font-medium rounded-lg border border-gray-200 transition-all hover:shadow-md text-sm cursor-pointer">
          <svg class="w-5 h-5 shrink-0" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/>
            <path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/>
            <path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/>
            <path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/>
          </svg>
          Se connecter avec Google
        </button>

        <button @click="signInWithGitHub" type="button"
          class="w-full flex items-center justify-center gap-3 px-4 py-3 bg-[#24292e] hover:bg-[#1a1e22] text-white font-medium rounded-lg transition-all hover:shadow-lg text-sm cursor-pointer border-none">
          <svg class="w-5 h-5 shrink-0" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" fill="currentColor">
            <path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.605-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/>
          </svg>
          Se connecter avec GitHub
        </button>

        <button @click="signInWithDiscord" type="button"
          class="w-full flex items-center justify-center gap-3 px-4 py-3 bg-[#5865F2] hover:bg-[#4752c4] text-white font-medium rounded-lg transition-all hover:shadow-lg text-sm cursor-pointer border-none">
          <svg class="w-5 h-5 shrink-0" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" fill="currentColor">
            <path d="M20.317 4.37a19.791 19.791 0 0 0-4.885-1.515.074.074 0 0 0-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 0 0-5.487 0 12.64 12.64 0 0 0-.617-1.25.077.077 0 0 0-.079-.037A19.736 19.736 0 0 0 3.677 4.37a.07.07 0 0 0-.032.027C.533 9.046-.32 13.58.099 18.057c.001.022.015.044.03.056a19.9 19.9 0 0 0 5.993 3.03.077.077 0 0 0 .084-.028 14.09 14.09 0 0 0 1.226-1.994.076.076 0 0 0-.041-.106 13.107 13.107 0 0 1-1.872-.892.077.077 0 0 1-.008-.128 10.2 10.2 0 0 0 .372-.292.074.074 0 0 1 .077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 0 1 .078.01c.12.098.246.198.373.292a.077.077 0 0 1-.006.127 12.299 12.299 0 0 1-1.873.892.077.077 0 0 0-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 0 0 .084.028 19.839 19.839 0 0 0 6.002-3.03.077.077 0 0 0 .032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 0 0-.031-.03zM8.02 15.33c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.956-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.956 2.418-2.157 2.418zm7.975 0c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.955-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.946 2.418-2.157 2.418z"/>
          </svg>
          Se connecter avec Discord
        </button>
      </div>

      <div class="mt-6 p-4 rounded-xl bg-green-950/80 border border-green-700/40">
        <h3 class="text-green-400 font-semibold text-sm mb-2">💡 Démo JWT</h3>
        <p class="text-green-600 text-xs leading-relaxed">
          ✅ Après connexion, un <strong class="text-green-300">Access Token</strong> JWT est stocké<br>
          ✅ Ce token est envoyé dans le header <code class="bg-green-950 px-1 rounded border border-green-700 text-green-400">Authorization: Bearer ...</code><br>
          ✅ Le serveur vérifie le token sans consulter de session
        </p>
      </div>

    </div>
  </div>
</template>

<script>
import { authService } from '../services/api'

export default {
  name: 'Login',
  data() {
    return {
      form: { email: '', password: '' },
      error: null,
      success: null,
      loading: false
    }
  },
  mounted() {
    const error = this.$route.query.error
    if (error === 'google_auth_failed') this.error = "Échec de l'authentification Google"
    else if (error === 'token_generation_failed') this.error = 'Erreur lors de la génération du token'
  },
  methods: {
    async handleLogin() {
      this.error = null; this.success = null; this.loading = true
      try {
        const response = await authService.login(this.form)
        this.success = response.message
        setTimeout(() => { this.$router.push('/home') }, 1000)
      } catch (err) {
        this.error = err.response?.data?.message || 'Erreur lors de la connexion'
      } finally { this.loading = false }
    },
    signInWithGoogle() { window.location.href = `${import.meta.env.VITE_API_URL}/auth/google` },
    signInWithGitHub() { window.location.href = `${import.meta.env.VITE_API_URL}/auth/github` },
    signInWithDiscord() { window.location.href = `${import.meta.env.VITE_API_URL}/auth/discord` },
  }
}
</script>
