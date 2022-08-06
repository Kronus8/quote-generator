<template>
    <div class="flex justify-center items-center h-screen bg-slate-200 dark:bg-base-100">
        <div class="card w-96 bg-slate-400 dark:bg-neutral text-neutral-content shadow-xl">
            <div class="card-body items-center text-center text-slate-900 dark:text-slate-200">
                <p>{{ quote.data.content }}</p>
                <h2 class="card-title">{{ quote.data.author || "Click to get a quote!" }}</h2>
                <div class="card-actions justify-end">
                <button class="btn btn-primary" @click="generate">New Quote</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
  import { onMounted, reactive } from 'vue'

  const quote = reactive({data:{content: '', author: ''}})

  async function generate() {
    await fetch('https://api.quotable.io/random').then(response => response.json()).then(result => {
      quote.data = result
    }); 
  };
  
  onMounted(() => {
    generate();
  })
</script>