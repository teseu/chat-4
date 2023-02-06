<script setup lang="ts">
import { reactive, computed } from 'vue'

import FirstChat from '@/components/FirstChat.vue'

const state = reactive({
  chat1: [],
  chat2: [],
})

const addChat = (msg: string, sender: object) => {
  state.chat1.push({
    msg: msg,
    sender: sender,
  })
  console.log('msg', msg, sender)
  console.log(state.chat1)

  state.chat2.push({
    msg: msg,
    sender: sender,
  })
  console.log('msg', msg, sender)
  console.log(state.chat1)
}

const Msgs1 = computed(() => {
  return state.chat1
})

const Msgs2 = computed(() => {
  return state.chat2
})
</script>

<template>
  <main class="bg-slate-900 h-screen w-screen">
    <div class="h-full grid place-content-center">
      <div class="container">
        <div class="mobile h-full flex flex-col justify-between">
          <div class="flex justify-between w-full">
            <div class="flex justify-start">
              <img
                src="@/assets/teseu.jpg"
                alt="Teseu"
                class="rounded-full h-10 w-10"
              />
              <div class="flex flex-col justify-end ml-3">
                <h1 class="text-white text-base font-bold">Teseu</h1>
                <p class="text-green-600 text-sm">
                  <span class="text-xs">🟢</span> Online
                </p>
              </div>
            </div>
            <div class="text-right text-white text-xl mt-2 w-3.5">x</div>
          </div>
          <p class="mt-4 text-center text-sm">Hoje 11:30</p>
          <div
            v-for="chat in Msgs1"
            :key="chat.msg"
            class="flex flex-col flex-wrap"
            :class="{
              'content-end': chat.sender.origin === 'mobile',
              'content-start': chat.sender.origin === 'desktop' }"
          >
          <div v-if="chat.sender.origin === 'mobile'" class="w-4/5">
            <p class="text-sm text-end px-3">Você - 10:32</p>
            <p class="m-3 px-3 py-2 w-full rounded-t-lg text-white text-end font-medium rounded-bl-lg bg-teal-600">
              {{ chat.msg }}
            </p>
          </div>
          <div v-else-if="chat.sender.origin === 'desktop'" class="w-4/5">
            <p class="text-sm text-start px-3">Teseu - 10:32</p>
            <p class="m-3 px-3 py-2 w-full rounded-t-lg text-white text-start font-medium rounded-br-lg bg-purple-600">
              {{ chat.msg }}
            </p>
          </div>
          </div>
          <FirstChat
            :sender="{
              origin: 'mobile',
              sendTo: 1,
            }"
            @add-chat="addChat"
          />
        </div>
        <div class="desktop h-full flex flex-col justify-between">
          <div class="flex justify-between w-full px-3">
            <div class="flex justify-start">
              <img
                src="@/assets/cecilia.png"
                alt="Cecilia Sassaki"
                class="rounded-full h-10 w-10"
              />
              <div class="flex flex-col justify-end ml-3">
                <h1 class="text-white text-base font-bold">Cecilia Sassaki</h1>
                <p class="text-green-600 text-sm">
                  <span class="text-xs">🟢</span> Online
                </p>
              </div>
            </div>
            <div class="text-right text-white text-xl mt-2 w-3.5">x</div>
          </div>
          <p class="mt-4 text-center text-sm">Hoje 11:30</p>
          <div
            v-for="chat in Msgs2"
            :key="chat.msg"
            class="flex flex-col flex-wrap"
            :class="{
              'content-end': chat.sender.origin === 'desktop',
              'content-start': chat.sender.origin === 'mobile' }"
          >
          <div v-if="chat.sender.origin === 'desktop'" class="w-3/5">
            <p class="text-sm text-end px-3">Você - 10:32</p>
            <p class="m-3 px-3 py-2 w-full rounded-t-lg text-white text-end font-medium rounded-bl-lg bg-teal-600">
              {{ chat.msg }}
            </p>
          </div>
          <div v-else-if="chat.sender.origin === 'mobile'" class="w-3/5">
            <p class="text-sm text-start px-3">Cecilia - 10:32</p>
            <p class="m-3 px-3 py-2 w-full rounded-t-lg text-white text-start font-medium rounded-br-lg bg-purple-600">
              {{ chat.msg }}
            </p>
          </div>
          </div>
          <FirstChat
            :sender="{
              origin: 'desktop',
              sendTo: 2,
            }"
            @add-chat="addChat"
          />
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped></style>
