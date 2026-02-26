<template>
  <div class="min-h-screen bg-green-950 p-6">
    <nav class="flex justify-between items-center bg-green-900 p-4 rounded-xl shadow-lg border border-green-800 mb-8">
      <h2 class="text-xl font-bold text-green-50 m-0">🏠 Accueil</h2>
      <button @click="handleLogout" class="px-4 py-2 bg-red-900/50 hover:bg-red-800/50 text-red-200 border border-red-800/50 rounded-lg transition-all cursor-pointer text-sm font-medium">Déconnexion</button>
    </nav>

    <div class="max-w-3xl mx-auto">
      <h1 class="text-3xl font-bold text-green-50 mb-8 text-center">Bienvenue {{ user?.name }} !</h1>

      <div v-if="error" class="mb-6 px-4 py-3 rounded-lg bg-red-500/10 border border-red-500/20 text-red-400">{{ error }}</div>

      <div class="bg-green-900 border border-green-800 rounded-2xl shadow-xl p-6 mb-6" v-if="profile">
        <h2 class="text-xl font-semibold text-green-300 mb-4 border-b border-green-800 pb-2">📋 Profil utilisateur</h2>
        <div class="space-y-3 text-green-100">
          <p><strong class="text-green-400 w-32 inline-block">ID:</strong> {{ profile._id }}</p>
          <p><strong class="text-green-400 w-32 inline-block">Nom:</strong> {{ profile.name }}</p>
          <p><strong class="text-green-400 w-32 inline-block">Email:</strong> {{ profile.email }}</p>
          <p><strong class="text-green-400 w-32 inline-block">Membre depuis:</strong> {{ formatDate(profile.createdAt) }}</p>
        </div>
      </div>

      <div class="bg-green-900 border border-green-800 rounded-2xl shadow-xl p-6">
        <h3 class="text-xl font-semibold text-green-300 mb-4 border-b border-green-800 pb-2">🔑 Informations JWT</h3>
        <div class="space-y-3 text-green-100">
          <p><strong class="text-green-400">Token stocké dans:</strong> <code class="bg-green-950 px-2 py-1 rounded border border-green-700 text-green-300 text-sm">localStorage.getItem('accessToken')</code></p>
          <p><strong class="text-green-400">Token utilisé:</strong> Header <code class="bg-green-950 px-2 py-1 rounded border border-green-700 text-green-300 text-sm">Authorization: Bearer [TOKEN]</code></p>
          <p><strong class="text-green-400">Expiration:</strong> {{ tokenExpiry }}</p>
          <p><strong class="text-green-400">Pas de session serveur:</strong> ✅ Stateless</p>

          <div class="mt-4 p-4 bg-green-950 rounded-xl border border-green-800 break-all text-xs text-green-500 font-mono">
            <strong class="text-green-400 block mb-2">Token (tronqué):</strong>
            <code>{{ truncatedToken }}</code>
          </div>
        </div>
      </div>

      <div class="text-center mt-8">
        <button @click="fetchProfile" class="px-6 py-3 bg-green-600 hover:bg-green-500 text-white font-semibold rounded-lg transition-all hover:shadow-lg hover:shadow-green-500/30 cursor-pointer border-none">
          🔄 Recharger le profil
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
      tokenExpiry: '1 heure'
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
      try {
        const response = await authService.getProfile()
        this.profile = response.user
      } catch (err) {
        this.error = err.response?.data?.message || 'Erreur lors du chargement du profil'
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
