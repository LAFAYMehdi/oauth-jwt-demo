<template>
  <div class="min-h-screen bg-lime-50 p-6 text-slate-900">
    <nav class="flex justify-between items-center bg-white p-4 rounded-xl shadow-md border border-lime-200 mb-8">
      <h2 class="text-xl font-bold text-lime-800 m-0">Accueil</h2>
      <button @click="handleLogout" class="px-4 py-2 bg-white hover:bg-lime-50 text-red-700 border border-red-200 rounded-lg transition-all cursor-pointer text-sm font-medium">Déconnexion</button>
    </nav>

    <div class="max-w-3xl mx-auto">
      <h1 class="text-3xl font-bold text-lime-900 mb-8 text-center">Bienvenue {{ user?.name }} !</h1>

      <div v-if="error" class="mb-6 px-4 py-3 rounded-lg bg-red-50 border border-red-200 text-red-700">{{ error }}</div>

      <div class="bg-white border border-lime-200 rounded-2xl shadow-xl p-6 mb-6" v-if="profile">
        <h2 class="text-xl font-semibold text-lime-800 mb-4 border-b border-lime-200 pb-2">Profil utilisateur</h2>
        <div class="space-y-3 text-slate-900">
          <p><strong class="text-lime-700 w-32 inline-block">ID:</strong> {{ profile._id }}</p>
          <p><strong class="text-lime-700 w-32 inline-block">Nom:</strong> {{ profile.name }}</p>
          <p><strong class="text-lime-700 w-32 inline-block">Email:</strong> {{ profile.email }}</p>
          <p><strong class="text-lime-700 w-32 inline-block">Membre depuis:</strong> {{ formatDate(profile.createdAt) }}</p>
        </div>
      </div>

      <div class="bg-white border border-lime-200 rounded-2xl shadow-xl p-6">
        <h3 class="text-xl font-semibold text-lime-800 mb-4 border-b border-lime-200 pb-2">Informations JWT</h3>
        <div class="space-y-3 text-slate-900">
          <p><strong class="text-lime-700">Token stocké dans:</strong> <code class="bg-lime-50 px-2 py-1 rounded border border-lime-200 text-slate-800 text-sm">localStorage.getItem('accessToken')</code></p>
          <p><strong class="text-lime-700">Token utilisé:</strong> Header <code class="bg-lime-50 px-2 py-1 rounded border border-lime-200 text-slate-800 text-sm">Authorization: Bearer [TOKEN]</code></p>
          <p><strong class="text-lime-700">Expiration:</strong> {{ tokenExpiry }}</p>
          <p><strong class="text-lime-700">Pas de session serveur:</strong> Stateless</p>

          <div class="mt-4 p-4 bg-lime-50 rounded-xl border border-lime-200 break-all text-xs text-slate-800 font-mono">
            <strong class="text-slate-900 block mb-2">Token (tronqué):</strong>
            <code>{{ truncatedToken }}</code>
          </div>
        </div>
      </div>

      <div class="text-center mt-8">
        <button
          @click="fetchProfile"
          :disabled="loading"
          class="inline-flex items-center justify-center gap-2 px-6 py-3 bg-lime-600 hover:bg-lime-700 disabled:opacity-60 disabled:cursor-not-allowed text-white font-semibold rounded-lg transition-all hover:shadow-lg hover:shadow-lime-600/30 cursor-pointer border-none"
        >
          <span v-if="loading" class="h-4 w-4 border-2 border-white/70 border-t-transparent rounded-full animate-spin"></span>
          <span>{{ loading ? 'Rechargement...' : 'Recharger le profil' }}</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { authService } from '../services/api'

export default {
  name: 'Home',
  data() {
    return {
      user: null,
      profile: null,
      error: null,
      tokenExpiry: '1 heure',
      loading: false
    }
  },
  computed: {
    truncatedToken() {
      const token = localStorage.getItem('accessToken')
      if (!token) return 'Aucun token'
      return token.substring(0, 50) + '...' + token.substring(token.length - 20)
    }
  },
  mounted() {
    this.user = authService.getCurrentUser()
    this.fetchProfile()
  },
  methods: {
    async fetchProfile() {
      this.error = null
      this.loading = true
      try {
        const response = await authService.getProfile()
        this.profile = response.user
      } catch (err) {
        this.error = err.response?.data?.message || 'Erreur lors du chargement du profil'
      } finally {
        this.loading = false
      }
    },
    handleLogout() {
      authService.logout()
      this.$router.push('/login')
    },
    formatDate(dateString) {
      return new Date(dateString).toLocaleString('fr-FR')
    }
  }
}
</script>
