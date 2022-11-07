<script setup lang="ts">
import { defineComponent, ref } from 'vue'

const pelanggan = ref(); 
//buat array kosong untuk menampung data pelanggan
const dataPelanggan = ref<number[][]>([]);
function handleClick() {
  dataPelanggan.value = [];
  for(let i = 0; i < pelanggan.value; i++) {
    dataPelanggan.value.push([i + 1, 0, 0, 0, 0, 0, 0]);
  }
  console.log(dataPelanggan.value);
}

function berubah() {
  for (let data = 0; data < pelanggan.value; data++) {
    dataPelanggan.value[data][4] = dataPelanggan.value[data][3] - dataPelanggan.value[data][2];
    dataPelanggan.value[data][5] = dataPelanggan.value[data][2] - dataPelanggan.value[data][1];
    // pelanggan diam
    if(data == pelanggan.value - 1) {
      dataPelanggan.value[data][6] = 0;
    } else {
      dataPelanggan.value[data][6] = Math.abs(dataPelanggan.value[data + 1][2] - dataPelanggan.value[data][3]);
    }
    
  }
}

</script>

<template>
  <div class="container">
    <form class="d-flex mb-4">
        <input class="form-control me-2" type="search" v-model="pelanggan" placeholder="Search" aria-label="Search">
        <button class="btn btn-outline-success" type="button" @click="handleClick()">Search</button>
      </form>
  </div>
  <div class="container">
    <table class="table table-hover table-striped table-bordered align-middle">
      <thead>
        <tr class="text-center">
          <th>Pelanggan</th>
          <th>Waktu Kedatangan</th>
          <th>Mulai Pelayanan</th>
          <th>Selesai Pelayanan</th>
          <th>Lama Pelanggan</th>
          <th>Pelanggan Menunggu</th>
          <th>Petugas Diam</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(i) in dataPelanggan">
          <th>{{ i[0] }}</th>
          <th><input type="text" class="form-control" v-model="i[1]" @change="berubah"></th>
          <th><input type="text" class="form-control" v-model="i[2]" @change="berubah"></th>
          <th><input type="text" class="form-control" v-model="i[3]" @change="berubah"></th>
          <th>{{ i[4] }}</th>
          <th>{{ i[5] }}</th>
          <th>{{ i[6] }}</th>
        </tr>
      </tbody>
    </table>

  </div>

</template>

