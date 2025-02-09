<script setup>
import { ref } from 'vue'
import { useFirebase } from '@/hooks/useFirebase'

import UiCard from '@/components/_ui/uiCard.vue'

const props = defineProps({
  data: Object
})

const auth = useFirebase()
const dialog = ref(false)
</script>

<template>
  <div v-if="props.data" class="position-relative">
    <v-row class="page-nav justify-center">
      <v-col cols="12" class="d-flex py-1">
        <v-btn icon="mdi-arrow-left" size="small" @click="$router.back()" />
      </v-col>
    </v-row>
    <v-row class="justify-center">
      <v-col cols="12" lg="10" sm="12">
        <ui-card :item="props.data" size="lg" />
      </v-col>
    </v-row>
    <v-row class="justify-center">
      <v-col cols="12" lg="7" sm="8" class="card-info">
        <v-card v-if="props.data.salary" class="pa-2" rounded="xl">
          <span class="text-h5 font-weight-bold px-2">{{ props.data.salary }}</span>
        </v-card>
        <v-hover v-slot="{ isHovering, props }">
          <v-card
            v-bind="props"
            class="blue-banner mt-2 pa-2"
            rounded="xl"
            :elevation="isHovering ? 10 : 1"
            href="https://yourcodereview.com/"
          >
            <v-card-title class="d-flex align-center font-weight-bold">
              Как зарабатывать больше?
              <v-icon class="ml-auto" color="white" icon="mdi-arrow-right" />
            </v-card-title>
            <v-card-text> Расскажем в наших карьерных консультациях </v-card-text>
          </v-card>
        </v-hover>
        <v-card v-if="props.data.description" class="mt-2 pa-6" rounded="xl">
          <div class="description" v-html="props.data.description" />
        </v-card>
      </v-col>
      <v-col cols="12" lg="3" sm="4">
        <v-card class="pa-4 d-flex flex-column" rounded="xl">
          <v-card-title class="pa-0 pb-1 font-weight-bold">Отклик</v-card-title>
          <v-btn block size="large" class="card-btn__purple mb-2" rounded="lg">
            Турбо отклик
            <v-dialog v-model="dialog" activator="parent" width="auto">
              <v-card class="pa-4" rounded="xl" max-width="600">
                <v-img src="@/assets/images/popup.png" />
                <h2 class="pa-2 text-h4 font-weight-bold">
                  Поможем откликнуться и сопроводим на всех этапах
                </h2>
                <p class="pa-2 text-h6 mb-4">
                  71% наших клиентов находят работу за 3 месяца. Среднее время поиска - 57 дней
                </p>
                <v-btn
                  height="60"
                  href="https://yourcodereview.com"
                  color="black"
                  size="large"
                  rounded="xl"
                  block
                  target="_blank"
                >
                  Узнать подробнее
                </v-btn>
                <v-btn class="close-popup" size="small" icon="mdi-close" @click="dialog = false" />
              </v-card>
            </v-dialog>
          </v-btn>
          <v-btn
            v-if="auth.isLoggedIn.value"
            block
            color="black"
            size="large"
            :href="props.data.url"
          >
            Отклик
          </v-btn>
          <v-btn v-else :to="{ name: 'Login' }" color="black" size="large" rounded="lg" block>
            Отклик
          </v-btn>
        </v-card>
      </v-col>
      <v-col cols="12" lg="10" sm="12">
        <v-card class="lime-banner pa-6" rounded="xl">
          <h2 class="pa-2 text-h4 font-weight-bold">Поможем найти работу за 3 месяца</h2>
          <p class="pa-2 text-h6 mb-4">
            71% наших клиентов находят работу за 3 месяца. Среднее время поиска - 57 дней
          </p>
          <v-btn color="black" rounded="xl" size="x-large" href="https://yourcodereview.com/"
            >Узнать подробнее</v-btn
          >
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<style scoped>
.card-info {
  display: flex;
  flex-direction: column;
  gap: 12px;
}
.close-popup {
  position: absolute;
  top: 25px;
  right: 25px;
}

.card-btn__purple {
  color: white;
  background-image: var(--purple-gradient);
}

.blue-banner {
  cursor: pointer;

  color: white;
  background-image: var(--blue-gradient);
}

.page-nav {
  position: sticky;
  z-index: 1006;
  top: 90px;

  border-radius: 50px;
}

.lime-banner {
  background-image: var(--lime-gradient);
}

.description {
  display: flex;
  flex-direction: column;

  gap: 16px;
}

.description > ul,
.description > ol {
  padding-left: 16px;
}
</style>
