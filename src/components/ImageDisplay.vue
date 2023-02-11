<template>
  <div>
    <div v-if="loading">
      <p>Loading...</p>
    </div>
    <div v-else>
      <img :src="imageUrl" />
    </div>
    <div>
      <input v-model="promptInput" placeholder="Enter prompt here" />
      <button @click="submitPrompt">Submit</button>
    </div>
  </div>
</template>
<script lang="ts">
import { Configuration, OpenAIApi } from "openai";

export default {
  name: "ImageDisplay",
  data() {
    return {
      imageUrl: "",
      promptInput: "",
      loading: false,
    };
  },
  methods: {
    async submitPrompt() {
      this.loading = true;
      const configuration = new Configuration({
        apiKey: "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",
      });
      const openai = new OpenAIApi(configuration);
      const response = await openai.createImage({
        prompt: this.promptInput,
        n: 2,
        size: "1024x1024",
      });
      this.loading = false;
      const imageUrl = response.data.data[0].url;
      if (imageUrl) {
        this.imageUrl = imageUrl;
      }
    },
  },
};
</script>



