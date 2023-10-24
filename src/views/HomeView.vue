<script setup>
import { useCounterStore } from "@/store/counter";
import { storeToRefs } from "pinia";

const userCounter = useCounterStore();

const { increment, discrement } = userCounter;
const { count, double, half } = storeToRefs(userCounter);
</script>

<template>
  <main>
    <!--
      <h1>Home counter: {{ userCounter.count }}</h1>
      <h2>Double: {{ userCounter.double }}</h2>
      <h2>half: {{ userCounter.half }}</h2>
      <button @click="userCounter.increment">Increment</button>
      <button @click="userCounter.discrement">Discrement</button>
    -->

    <h1>Home counter: {{ count }}</h1>
    <h2>Double: {{ double }}</h2>
    <h2>half: {{ half }}</h2>
    <button @click="increment">Increment</button>
    <button @click="discrement">Discrement</button>
  </main>
</template>
