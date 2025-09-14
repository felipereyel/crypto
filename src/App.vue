<script setup lang="ts">
import CryptoJS from "crypto-js";
import { ref } from 'vue';

const plaintext = ref('');
const ciphertext = ref('');
const key = ref('');

function encrypt(plainText: string, key: string): string {
    return CryptoJS.AES.encrypt(plainText, key).toString();
}

function decrypt(cipherText: string, key: string): string {
    const bytes = CryptoJS.AES.decrypt(cipherText, key);
    return bytes.toString(CryptoJS.enc.Utf8);
}

function onEncrypt() {
  if (!key.value) {
    alert('Please enter a secret key.');
    return;
  }
  ciphertext.value = encrypt(plaintext.value, key.value);
}

function onDecrypt() {
  if (!key.value) {
    alert('Please enter a secret key.');
    return;
  }
  plaintext.value = decrypt(ciphertext.value, key.value);
}
</script>

<template>
  <main class="crypto-main">
    <div class="crypto-areas">
      <div class="crypto-block">
        <h2>Ciphertext</h2>
        <textarea v-model="ciphertext" class="crypto-textarea" placeholder="Ciphertext"></textarea>
      </div>
      <div class="crypto-block">
        <h2>Plaintext</h2>
        <textarea v-model="plaintext" class="crypto-textarea" placeholder="Plaintext"></textarea>
      </div>
    </div>
    <!-- Secret input and buttons will be added below -->
    <div class="crypto-controls">
      <input
        v-model="key"
        type="password"
        class="crypto-key-input"
        placeholder="Enter secret key"
      />
      <div class="crypto-buttons">
        <button @click="onEncrypt" class="crypto-btn encrypt">Encrypt</button>
        <button @click="onDecrypt" class="crypto-btn decrypt">Decrypt</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
html, body, #app, .crypto-main {
  width: 100vw;
  min-height: 100vh;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.crypto-main {
  display: flex;
  flex-direction: column;
  align-items: stretch;
  justify-content: flex-start;
  min-height: 100vh;
  width: 100vw;
  background: var(--bg-gradient, linear-gradient(135deg, #18181b 0%, #1e293b 100%));
  padding: 2rem 0 0 0;
}
.crypto-areas {
  display: flex;
  gap: 2rem;
  margin-bottom: 2rem;
  width: 100vw;
  justify-content: center;
}
.crypto-block {
  display: flex;
  flex-direction: column;
  align-items: stretch;
  flex: 1 1 0;
  max-width: 700px;
  min-width: 320px;
  padding: 0 2vw;
}
.crypto-block h2 {
  margin-bottom: 0.5rem;
  color: #2563eb;
  font-size: 1.2rem;
}
.crypto-textarea {
  width: 100%;
  min-width: 0;
  height: 40vh;
  border-radius: 8px;
  border: 1px solid var(--block-border, #334155);
  padding: 1rem;
  font-size: 1.1rem;
  background: var(--block-bg, #23272f);
  color: var(--text-main, #f1f5f9);
  box-shadow: var(--block-shadow, 0 2px 12px 0 #0008);
  resize: vertical;
  margin-bottom: 0.5rem;
}
.crypto-controls {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  width: 100vw;
  max-width: 100vw;
}
.crypto-key-input {
  padding: 0.75rem 1rem;
  border-radius: 6px;
  border: 1px solid #cbd5e1;
  font-size: 1rem;
  width: 260px;
  background: #f8fafc;
  margin-bottom: 0.5rem;
}
.crypto-buttons {
  display: flex;
  gap: 1.5rem;
}
.crypto-btn {
  padding: 0.7rem 1.5rem;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s, color 0.2s;
}
.crypto-btn.encrypt {
  background: #2563eb;
  color: #fff;
}
.crypto-btn.decrypt {
  background: #f59e42;
  color: #fff;
}
.crypto-btn:hover {
  filter: brightness(1.1);
}
</style>
