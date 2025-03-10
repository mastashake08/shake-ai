<script setup>
import { ref } from "vue";

const systemPrompt = ref("");
const userMessage = ref("");
const responseText = ref("");
const isLoading = ref(false);
let session = null;

const startSession = async () => {
  if (!systemPrompt.value) return alert("Please enter a system prompt!");
  try {
    session = await chrome.aiOriginTrial.languageModel.create({
      systemPrompt: systemPrompt.value,
      monitor(m) {
          m.addEventListener("downloadprogress", (e) => {
          responseText.value = (`Downloaded ${e.loaded} of ${e.total} bytes.`);
          });
          },
      });
  } catch (error) {
    responseText.value += error.message;
  }
}

const sendPrompt = async () => {
  if (!session) return alert("Start a session first!");
  if (!userMessage.value) return;

  responseText.value = "";
  isLoading.value = true;

  const stream = session.promptStreaming(userMessage.value);
  let previousChunk = '';

  for await (const chunk of stream) {
    const newChunk = chunk.startsWith(previousChunk)
        ? chunk.slice(previousChunk.length) : chunk;
    console.log(newChunk);
    responseText.value  += newChunk;
    previousChunk = chunk;
    
  }

  isLoading.value = false;
};
</script>

<template>
  <div class="min-h-screen flex flex-col items-center justify-center bg-gray-900 text-white p-6 mr-4">
    <h1 class="text-3xl font-bold mb-4">Shake AI 🤖</h1>

    <!-- System Prompt Input -->
    <div class="w-full max-w-lg">
      <label class="block text-lg mb-2">System Prompt:</label>
      <textarea v-model="systemPrompt" class="w-full p-2 rounded bg-gray-800 border border-gray-700"></textarea>
      <button
        @click="startSession"
        class="mt-2 w-full py-2 bg-blue-600 hover:bg-blue-500 rounded text-white font-semibold"
      >
        Start Session
      </button>
    </div>

    <!-- User Message Input -->
    <div class="w-full max-w-lg mt-6">
      <label class="block text-lg mb-2">Your Message:</label>
      <input v-model="userMessage" type="text" class="w-full p-2 rounded bg-gray-800 border border-gray-700" />
      <button
        @click="sendPrompt"
        class="mt-2 w-full py-2 bg-green-600 hover:bg-green-500 rounded text-white font-semibold"
      >
        Send
      </button>
    </div>

    <!-- AI Response -->
    <div class="w-full max-w-lg mt-6 mb-4 p-4 bg-gray-800 rounded border border-gray-700">
      <p class="text-lg font-semibold">Response:</p>
      <div class="response-text mt-2 mb-2 text-gray-300 whitespace-pre-line">{{ responseText || "Waiting for response..." }}</div>
      <div v-if="isLoading" class="mt-2 text-yellow-400">Loading...</div>
    </div>
  </div>
</template>

<style>
/* Tailwind will handle most of the styling */
.response-text {
  max-height: auto; /* Adjusted height for better fit in popup */
  overflow-y: auto;
}
</style>
