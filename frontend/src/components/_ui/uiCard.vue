<script setup>
defineProps({
  item: Object,
  size: {
    type: String,
    default: 'md'
  }
})
</script>

<template>
  <v-hover v-slot="{ isHovering, props }">
    <!-- <template v-if="size === 'lg'">
      <v-img v-if="item.internship" max-height="100" cover src="@/assets/images/intern.jpg" />
      <v-img v-else max-height="100" cover src="@/assets/images/experience.jpg"></v-img>
    </template> -->
    <v-card
      v-bind="props"
      min-height="155"
      class="card py-4 mx-auto"
      :class="`card-${size}`"
      :elevation="isHovering && size === 'md' ? 10 : 1"
      rounded="xl"
    >
      <v-card-subtitle class="font-weight-bold">{{ item?.company_name }}</v-card-subtitle>
      <v-card-title
        v-if="item.title"
        class="font-weight-bold"
        :class="size === 'lg' ? 'text-h5' : ''"
        >{{ item.title }}</v-card-title
      >
      <v-chip-group
        v-if="item.remote || item.location || item.internship || item.salary"
        class="custom-chips"
      >
        <v-chip
          v-if="item.location"
          class="chip text-grey-darken-2"
          prepend-icon="mdi-map-marker"
          label
          >{{ item.location.split(',')[0] }}</v-chip
        >
        <v-chip
          v-if="item.remote"
          class="chip text-grey-darken-2"
          prepend-icon="mdi-briefcase"
          label
          >Удаленно</v-chip
        >
        <v-chip v-if="item.internship" class="chip chip-salary text-grey-darken-2" label
          >Стажировка</v-chip
        >
        
        <v-chip
          v-if="item.salary && size !== 'lg'"
          class="chip chip-salary text-grey-darken-2"
          label
          >{{ item.salary }}</v-chip
        >
      </v-chip-group>
    </v-card>
  </v-hover>
</template>

<style scoped>
.card-md {
  max-width: 600px;
  margin-bottom: 16px;
}
.card-lg {
  /* border-top-left-radius: 0 !important;
  border-top-right-radius: 0 !important; */
  max-width: 100%;
}
.custom-chips {
  padding: 0.5rem 1rem;
}

.card-md .chip-salary {
  margin-left: 0;
}

@media screen and (min-width: 1280px) {
  .card-md .chip-salary {
    margin-left: auto;
  }
}
</style>
