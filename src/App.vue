<script setup lang="ts">
import { RouterView, useRouter } from 'vue-router'
import { AppStore } from './modules/store/app'
import HomeIcon from './components/icons/HomeIcon.vue'
import ProductIcon from './components/icons/ProductIcon.vue'
import UsersIcon from './components/icons/UsersIcon.vue'
import InfoIcon from './components/icons/InfoIcon.vue'
import LogoutIcon from './components/icons/LogoutIcon.vue'

const router = useRouter()

function logout() {
  AppStore.set('auth', false)
  router.push('/')
}
</script>

<template>
  <main class="content">
    <RouterView v-slot="{ Component }">
      <Transition name="fade-slide" mode="out-in" appear>
        <component :is="Component" />
      </Transition>
    </RouterView>
  </main>

  <Transition name="fade-slide" mode="out-in" appear>
    <nav v-if="AppStore.state.auth">
      <RouterLink to="/sistema" title="Início">
        <HomeIcon class="icon" />
      </RouterLink>

      <RouterLink to="/sistema/produtos" title="Produtos">
        <ProductIcon class="icon" />
      </RouterLink>

      <RouterLink to="/sistema/clientes" title="Clientes">
        <UsersIcon class="icon" />
      </RouterLink>

      <RouterLink to="/sobre" title="Sobre">
        <InfoIcon class="icon" />
      </RouterLink>

      <button type="button" @click="logout">
        <LogoutIcon class="icon" />
      </button>
    </nav>
  </Transition>
</template>

<style lang="pcss" scoped>
main {
  @apply flex flex-col items-center justify-center mt-8 mb-32;
}

nav {
  @apply fixed bottom-4 left-1/2 transform -translate-x-1/2 z-10;
  @apply bg-white rounded-full shadow-lg px-5 py-4 border border-blue-700;
  @apply flex justify-center gap-8 text-3xl;

  a {
    @apply text-slate-500 hover:text-blue-900;

    &.router-link-exact-active {
      @apply text-blue-700;
    }
  }

  button {
    @apply text-red-700;
  }

  .icon {
    @apply relative bottom-0.5;
  }
}
</style>
