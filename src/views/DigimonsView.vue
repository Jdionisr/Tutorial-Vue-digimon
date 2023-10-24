<script setup>
import { RouterLink } from "vue-router";
import { useGetdata } from "../composables/getData";

const { data, getData, errorData } = useGetdata();

getData("https://www.digi-api.com/api/v1/digimon?pageSize=10");

const getNext = () => {
  if (data.value.pageable.nextPage) {
    getData(data.value.pageable.nextPage);
  }
};

const getPrevius = () => {
  if (data.value.pageable.previousPage) {
    getData(data.value.pageable.previousPage);
  }
};
</script>

<template>
  <div class="row justify-content-center">
    <div class="alert alert-danger" v-if="errorData">Error del servidor</div>
    <div class="col-6" v-else>
      <div class="row justify-content-center">
        <div class="col-3">
          <button
            class="btn btn-outline-success"
            @click="getPrevius"
            :disabled="!data?.pageable.previousPage"
          >
            Previus
          </button>
        </div>
        <div class="col-3">
          <button
            class="btn btn-outline-success"
            @click="getNext"
            :disabled="!data?.pageable.nextPage"
          >
            Next
          </button>
        </div>
      </div>
    </div>
  </div>
  <div class="row">
    <div class="col-12">
      <h1>Digimons</h1>
      <div class="row align-items-center justify-content-center">
        <div
          class="card col-2 mx-3 my-2"
          v-for="digimon in data?.content"
          style="height: 300px"
        >
          <img
            :src="digimon.image"
            class="card-img-top"
            :alt="digimon.name"
            style="max-width: 154px; max-height: 154px"
          />
          <div class="card-body">
            <h5 class="card-title">
              <router-link :to="`/digimons/${digimon.name}`">{{
                digimon.name
              }}</router-link>
            </h5>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
