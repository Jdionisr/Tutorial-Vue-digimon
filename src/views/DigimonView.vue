<script setup>
import { useRoute, useRouter } from "vue-router";
import { useGetdata } from "@/composables/getData";
import { useFavoritoStore } from "@/store/favoritos";

const router = useRouter();
const route = useRoute();
const { getData, data, errorData, loading } = useGetdata();
const useFavorito = useFavoritoStore;

const { add, findDigimon } = useFavorito();

const back = () => {
  router.push("/digimons");
};

getData(`https://www.digi-api.com/api/v1/digimon/${route.params.name}`);
</script>

<template>
  <div class="row align-items-center justify-content-center">
    <p v-if="loading">Cargando...</p>
    <div class="alert alert-danger" v-if="errorData">Elemento no existente</div>
    <div
      class="card col-12"
      style="background-color: rgb(231, 223, 213)"
      v-else
    >
      <h1 cl>{{ data?.name }}</h1>
      <div class="row justify-content-center mt-2">
        <img
          :src="data?.images[0].href"
          class="card-img-top"
          style="width: 25rem"
          :alt="data?.name"
        />
      </div>
      <h3>Description</h3>
      <template v-for="description in data?.descriptions">
        <p class="card-text" v-if="description.language === 'en_us'">
          {{ description.description }}
        </p>
      </template>
      <div class="row justify-content-center">
        <div class="col-4">Release Date: {{ data?.releaseDate }}</div>
        <div class="col-4">xAntibody: {{ data?.xAntibody }}</div>
      </div>

      <div class="row">
        <div class="col-3">
          <h5>Levels</h5>
          <ul class="list-group list-group-flush">
            <li
              class="list-group-item bg-color-customer"
              v-for="level in data?.levels"
            >
              {{ level.level }}
            </li>
          </ul>
        </div>
        <div class="col-3">
          <h5>Types</h5>
          <ul class="list-group list-group-flush">
            <li
              class="list-group-item bg-color-customer"
              v-for="tp in data?.types"
            >
              {{ tp.type }}
            </li>
          </ul>
        </div>
        <div class="col-3">
          <h5>Attributes</h5>
          <ul class="list-group list-group-flush">
            <li
              class="list-group-item bg-color-customer"
              v-for="attribute in data?.attributes"
            >
              {{ attribute.attribute }}
            </li>
          </ul>
        </div>
        <div class="col-3">
          <h5>Fields</h5>
          <ul class="list-group list-group-flush">
            <li
              class="list-group-item bg-color-customer"
              v-for="field in data?.fields"
            >
              {{ field.field }}
              <img :src="field.image" :alt="field.field" />
            </li>
          </ul>
        </div>
      </div>

      <div class="row justify-content-center">
        <h3>Skills</h3>
        <div
          class="col-3 card mx-1 my-1 bg-color-customer"
          v-for="skill in data?.skills"
        >
          <p class="card-text">{{ skill.skill }} - {{ skill.translation }}</p>
          <p class="card-text">
            {{ skill.description }}
          </p>
        </div>
      </div>
      <div class="row justify-content-center mb-2">
        <div class="col-2">
          <button type="button" class="btn btn-secondary" @click="back">
            volver
          </button>
        </div>
        <div class="col-2">
          <button
            type="button"
            class="btn btn-warning"
            @click="add(data)"
            :disabled="findDigimon(data.name)"
          >
            Agregar favotiro
          </button>
        </div>
      </div>
    </div>
  </div>
  <!--
  <div class="row align-items-center justify-content-center" >
    <h1>Elemento no existente</h1>
    <div class="row justify-content-center mb-2">
      <div class="col-2">
        <button type="button" class="btn btn-secondary" @click="back">
          volver
        </button>
      </div>
    </div>
  </div>
  -->
</template>

<style>
.bg-color-customer {
  background-color: rgb(169, 209, 196);
}
</style>
