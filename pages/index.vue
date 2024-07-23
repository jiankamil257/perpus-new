<template>
  <div class="container-fluid">
    <div class="row my-5">
      <div class="col-lg-6">
        <nuxt-link to="/pengunjung/tambah">
          <div class="card bg-pengunjung rounded-5">
            <div class="card-body">
              <h2>Pengunjung</h2>
            </div>
          </div>
        </nuxt-link>
      </div>

      <div class="col-lg-6">
        <nuxt-link to="/buku">
          <div class="card bg-buku rounded-5">
            <div class="card-body">
              <h2>Cari Buku</h2>
            </div>
          </div>
        </nuxt-link>
      </div>
    </div>
  </div>
  <h2 class="justify-content-between">STATISTIK</h2>
  <div class="container-fluid">
    <div class="row justify-content-evenly rounded-5">
      <div class="col-5">
        <div class="raccing">
          <h2>Pengunjung</h2>
        </div>
      </div>
      <div class="col-5">
        <div class="raccing1">
          <h2>Buku</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  height: 250px;
  box-shadow: 1px 1px 10px #424242;
}
.card.bg-pengunjung {
background-image: url('../assets/img/bg-home-kunjungan.jpeg');
background-repeat: no-repeat;
background-position: center center;
background-size: cover;
}
.card.bg-buku {
  background: url('../assets/img/bg-home-cari-buku.jpg') no-repeat center center;
  background-size: cover;
}

.raccing {
  height: 174px;
  box-shadow: 1px 1px 10px;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #BFDF7A;
}

.raccing1 {
  height: 174px;
  box-shadow: 1px 1px 10px;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #62E967;
}
</style>
<script setup>
const supabase = useSupabaseClient()
const books = ref([])
const visitors = ref ([])

const totalPengunjung = async () => {
  const { data, error } = await supabase.from('pengunjung').select(`*, keanggotaan(*), keperluan(*)`)
  if(data) visitors.value = data
}



const totalBuku = async () => {
  const { data, error } = await supabase.from('buku').select(`*, kategori(*)`)
  if(data) books.value = data
}

onMounted(() => {
  totalBuku()
  totalPengunjung()
})

</script>