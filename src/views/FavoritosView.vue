<script setup>
import { useFavoritoStore } from "@/store/favoritos";
import { storeToRefs } from "pinia";
import { RouterLink } from "vue-router";

const useFavorito = useFavoritoStore();

const { favoritos } = storeToRefs(useFavorito);

const { remove } = useFavorito;
</script>

<template>
  <h1 class="h1">Favoritos</h1>
  <p v-if="favoritos.length === 0">Sin favoritos</p>
  <div class="list-group" v-else>
    <div class="list-group-item" v-for="digimon in favoritos" :key="digimon.id">
      <div>
        {{ digimon.name }}
      </div>
      <div>
        <router-link
          class="btn btn-sm btn-outline-info mx-2"
          :to="`/digimons/${digimon.name}`"
          >Detalle</router-link
        >
        <button
          class="btn btn-outline-danger btn-sm"
          @click="remove(digimon.id)"
        >
          Eliminar
        </button>
      </div>
    </div>
  </div>
</template>
