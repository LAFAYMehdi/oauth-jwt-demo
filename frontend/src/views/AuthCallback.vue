<template>
  <div class="min-h-screen bg-lime-50 flex items-center justify-center p-4">
    <div class="bg-white border border-lime-200 rounded-2xl shadow-xl p-8 w-full max-w-md text-center">
      <div class="animate-spin rounded-full h-12 w-12 border-b-2 border-lime-500 mx-auto mb-4"></div>
      <h2 class="text-xl font-semibold text-lime-800">Authentification en cours...</h2>
      <p class="text-lime-600 mt-2 text-sm">Veuillez patienter pendant que nous vous connectons.</p>
    </div>
  </div>
</template>

<script>
import { authService } from '../services/api'

export default {
  name: 'AuthCallback',
  mounted() {
    // Récupère le token soit dans la query (?token=), soit dans le hash (#token=)
    const searchToken = new URLSearchParams(window.location.search).get('token')
    const hashToken = new URLSearchParams(window.location.hash.replace(/^#/, '?')).get('token')
    const token = searchToken || hashToken

    if (token) {
      authService.setToken(token)
      this.$router.push('/home')
    } else {
      // Pas de token reçu : renvoyer vers login après un bref délai
      setTimeout(() => {
        this.$router.push('/login?error=google_auth_failed')
      }, 800)
    }
  }
}
</script>
