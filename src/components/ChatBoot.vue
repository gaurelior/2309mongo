<template>
    <div>
      <label>Insira </label>
      <form @submit.prevent="handleSubmit">
        <textarea v-model="prompt" placeholder="Digite seu texto aqui"></textarea>
        <button type="submit">Enviar</button>
      </form>
      <div>
        <label>Resposta:</label>
        <textarea v-model="response" readonly></textarea>
      </div>
    </div>
  </template>
  
  <script>
  import { GoogleGenerativeAI } from "@google/generative-ai";
  
  export default {
    data() {
      return {
        prompt: "",
        response: "",
        genAI: null,
        model: null,
      };
    },
    created() {
      // Fetch your API_KEY
      const API_KEY = "AIzaSyCNLusWlSnMjFFzHNrbAf9aQ9zO-AyfM4s"; // Substitua pelo seu API_KEY
      this.genAI = new GoogleGenerativeAI(API_KEY);
      this.model = this.genAI.getGenerativeModel({ model: "gemini-1.5-flash" });
    },
    methods: {
      async handleSubmit() {
        try {
          const result = await this.model.generateContent(this.prompt);
          const text = await result.response.text();
          this.response = text;
        } catch (error) {
          console.error("Erro ao gerar conteúdo:", error);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  /* Adicione seu estilo aqui */
  </style>
  