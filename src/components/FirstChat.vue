<script setup lang="ts">
// import { defineEmits } from 'vue'
const props = defineProps({
  sender: {
    type: Object,
    origin: String,
    sendTo: Number,
  },
  msg: {
    type: String,
  },
})
const emit = defineEmits(['addChat'])
const onAddChat = (e) => {
  const msg = e.target.value
  emit('addChat', msg, props.sender)
  // emit('addChat', props.sender)
  e.target.value = ''
}
</script>

<template>
  <div class="px-3 mt-auto">
    <input
      type="text"
      sender="{sender.origin, sender.sendTo}"
      @keydown.enter="onAddChat"
      placeholder="Digite sua mensagem"
      class="form-control bg-slate-700 text-white leading-6 rounded-full px-3 py-3 w-full"
    />
  </div>
</template>
