<template>
  <v-form @submit.prevent="handleSubmit">
    <v-text-field v-model="form.title" label="Title" @keydown.enter.prevent="handleSubmit" autofocus @blur="$emit('onGoalTabPostBlur')"/>
  </v-form>
</template>

<script lang="ts" setup>
import { reactive } from 'vue'
import { useGoalsStore } from '~/store/goals'

const goalStore = useGoalsStore()
const emit = defineEmits(['onGoalTabPostBlur'])
const form = reactive({
  title: ''
})

const handleSubmit = () => {
  if (!form.title) return

  goalStore.add({
    title: form.title
  })
  form.title = ''
  emit('onGoalTabPostBlur')
}

</script>

<style scoped></style>
