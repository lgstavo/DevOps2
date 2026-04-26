<template>
  <div class="page-wrapper">
    <div class="card-container">
      <div class="page-title">
        <h2>Nova postagem</h2>
        <p>Compartilhe algo com seus amigos</p>
      </div>

      <div class="post-card">
        <textarea
          v-model="postContent"
          placeholder="No que você está pensando?"
          rows="5"
          maxlength="280"
        ></textarea>

        <div class="card-footer">
          <span :class="{ danger: postContent.length >= 280 }">
            {{ postContent.length }} / 280
          </span>
          <button @click="sendPost" :disabled="!postContent.trim()">
            Postar
          </button>
        </div>
      </div>

      <div v-if="successMsg" class="feedback success">Post enviado com sucesso!</div>
      <div v-if="error" class="feedback error">{{ error }}</div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import api from "@/services/api.js";

const postContent = ref('');
const error = ref(null);
const successMsg = ref(false);

async function sendPost() {
  if (!postContent.value.trim()) return;
  error.value = null;

  try {
    await api.post('/api/postagens', { descricao: postContent.value });
    postContent.value = '';
    successMsg.value = true;
    setTimeout(() => successMsg.value = false, 3000);
  } catch (err) {
    console.error('Erro ao enviar post:', err);
    error.value = 'Não foi possível enviar o post.';
  }
}
</script>

<style scoped>
.page-wrapper {
  min-height: 100vh;
  background-color: #f0f2f5;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
}

.card-container {
  width: 100%;
  max-width: 560px;
}

.page-title {
  text-align: center;
  margin-bottom: 1.5rem;
}

.page-title h2 {
  margin: 0;
  font-size: 1.4em;
  font-weight: 500;
  color: #1d2129;
}

.page-title p {
  margin: 6px 0 0;
  font-size: 0.9em;
  color: #888;
}

.post-card {
  background: #fff;
  border: 1px solid #e1e4e8;
  border-radius: 12px;
  padding: 1.5rem;
}

textarea {
  width: 100%;
  box-sizing: border-box;
  resize: none;
  border: 1px solid #e1e4e8;
  border-radius: 8px;
  padding: 12px;
  font-size: 15px;
  color: #1d2129;
  background: #f7f8fa;
  outline: none;
  line-height: 1.6;
  font-family: inherit;
}

textarea:focus {
  border-color: #007bff;
}

.card-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 12px;
}

.card-footer span {
  font-size: 13px;
  color: #aaa;
}

.card-footer span.danger {
  color: #dc3545;
}

button {
  padding: 10px 24px;
  border: none;
  border-radius: 8px;
  background-color: #007bff;
  color: white;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.2s;
}

button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

button:not(:disabled):hover {
  background-color: #0056b3;
}

.feedback {
  margin-top: 1rem;
  border-radius: 8px;
  padding: 12px 16px;
  font-size: 14px;
  text-align: center;
}

.feedback.success {
  background-color: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
}

.feedback.error {
  background-color: #f8d7da;
  color: #721c24;
  border: 1px solid #f5c6cb;
}
</style>