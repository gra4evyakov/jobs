<script setup>
import { ref, computed } from 'vue'
import { useFirebase } from '@/hooks/useFirebase'

import UiLoginButton from '@/components/_ui/uiLoginButton.vue'
import UiLogoutButton from '@/components/_ui/uiLogoutButton.vue'
import UiCareerButton from '@/components/_ui/uiCareerButton.vue'
import uiAddVacancyButton from '@/components/_ui/uiAddVacancyButton.vue'

defineProps({
  list: Array
})

const auth = useFirebase()
const menu = ref(false)

const showLoginButton = computed(() => !auth.isLoggedIn.value)
</script>

<template>
  <div class="text-center">
    <v-menu
      v-model="menu"
      :close-on-content-click="false"
      location="start"
      transition="slide-x-reverse-transition"
    >
      <template v-slot:activator="{ props }">
        <v-btn color="white" v-bind="props" icon>
          <v-icon>mdi-menu</v-icon>
        </v-btn>
      </template>
      <v-card class="d-flex flex-column align-center pa-4 bg-white" rounded="lg">
        <UiCareerButton variant="flat" block />
        <UiLoginButton v-if="showLoginButton" variant="flat" block />
        <UiLogoutButton v-else variant="flat" block />
        <slot />
        <uiAddVacancyButton variant="flat" block />
      </v-card>
    </v-menu>
  </div>
</template>
