<template>
  <h2 class="text-star my-4"> {{ buku.judul }}</h2>
  <div class="row">
    <div class="col-md-3">
      <img :src="buku?.cover" class="cover" alt="cover buku" style="width: 300px;">
    </div>
    <div class="col-lg-8 col-12">
      <div class="row">
        <h1>{{ buku?.judul }}</h1>
      </div>
      <div class="row">
        <h4>Pengarang : {{ buku?.penulis }}</h4>
        <h4>Penerbit : {{ buku?.penerbit }}</h4>
        <h4>Tahun Terbit : {{ buku?.tahun_terbit }}</h4>
        <h4>Genre : {{ buku?.genre }}</h4>
      </div>
      <div class="row">
        <h6>{{ buku?.deskripsi }}</h6>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';

const supabase = useSupabaseClient()

const route = useRoute()
const buku = ref([])


const getBookById = async () => {
  const { data, error } = await supabase.from('buku')
    .select(`*, kategori_buku(*)`)
    .eq('id', route.params.id)
    .maybeSingle()
  if (!error) buku.value = data
}

onMounted(() => {
  getBookById()
})
</script>

<style scoped>
.wrapper {
  color: #fffeee;
  letter-spacing: 1.2px;
}


.btn {
  background-color: #fffeee;
  font-family: 'Jockey One';
}

h1 {
  font-family: "Jockey One";
}

h4 {
  font-family: "Jaldi";
  font-size: 30px;
}

h6 {
  font-family: "Jaldi";
  font-size: 20px;
  letter-spacing: 2px;
}
</style>