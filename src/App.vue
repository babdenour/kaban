<script setup>
import AssemblyLine from './components/AssemblyLine.vue'
</script>

<template>
   <div id="vue-app">
    <AssemblyLine :stages='[
        "Idea", 
        "Development", 
        "Testing", 
        "Deployment"
      ]' 
    />
  </div>
</template>