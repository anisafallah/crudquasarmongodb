<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
  <q-page padding class="items-center-justify-center bg-grey-3">
    <q-card flat class="bg-white q-pa-md">
      <span class="text-h5 text-weight-light q-pa-md">
        <span class="text-blue-grey-14">Tambah Data Buku</span>
      </span>
      <div class="q-pa-md">
        <q-form
          @submit="onSubmit"
          class="q-gutter-md"
        >

          <q-input
            label="Kode Buku"
            lazy-rules
            color="teal"
            v-model="form.kodeBuku"
            :rules="[
           val => val !== null && val !== '' || 'Kode Buku Dibutuhkan'
           ]">
            <template v-slot:append>
              <q-icon name="dns"/>
            </template>
          </q-input>
          <q-input
            label="Judul Buku"
            lazy-rules
            color="teal"
            v-model="form.judulBuku"
            :rules="[
           val => val !== null && val !== '' || 'Judul Buku Dibutuhkan'
           ]">
            <template v-slot:append>
              <q-icon name="title"/>
            </template>
          </q-input>
          <q-input
            label="Penerbit"
            lazy-rules
            color="teal"
            v-model="form.penerbit"
            :rules="[
           val => val !== null && val !== '' || 'Penerbit Dibutuhkan'
           ]">
            <template v-slot:append>
              <q-icon name="menu_book"/>
            </template>
          </q-input>
          <q-input
            label="Pengarang"
            lazy-rules
            color="teal"
            v-model="form.pengarang"
            :rules="[
           val => val !== null && val !== '' || 'Pengarang Dibutuhkan'
           ]">
            <template v-slot:append>
              <q-icon name="person"/>
            </template>
          </q-input>
          <q-input
            label="Tahun Terbit"
            lazy-rules
            color="teal"
            v-model="form.tahunTerbit"
            :rules="[
           val => val !== null && val !== '' || 'Tahun Terbit Dibutuhkan'
           ]">
            <template v-slot:append>
              <q-icon name="calendar_today"/>
            </template>
          </q-input>

          <q-input
            label="Harga Buku"
            lazy-rules
            color="teal"
            v-model="form.hargaBuku"
            :rules="[
           val => val !== null && val !== '' || 'Tahun Terbit Dibutuhkan'
           ]">
            <template v-slot:append>
              <q-icon name="attach_money"/>
            </template>
          </q-input>

          <q-input
            lazy-rules
            hint="Pilih gambar"
            type="file"
            ref="file"
            @input="selectFile()"
            color="teal"
            :rules="[
           val => val !== null && val !== '' || 'Gambar Dibutuhkan'
           ]">
            <template v-slot:append>
              <q-icon name="add_photo_alternate"/>
            </template>
          </q-input>

          <div>
            <q-btn
              unelevated
              icon="add"
              label="Tambah Data Buku"
              style="height: 50px"
              type="submit"
              color="teal-6"/>
          </div>
        </q-form>
      </div>
    </q-card>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      form: {
        judulBuku: null,
        kodeBuku: null,
        penerbit: null,
        pengarang: null,
        tahunTerbit: null,
        hargaBuku: null
      },
      gambar: null
    }
  },
  methods: {
    selectFile () {
      this.gambar = this.$refs.file.$refs.input.files[0]
    },
    onSubmit () {
      const formData = new FormData()
      formData.append('gambar', this.gambar)
      formData.append('judulBuku', this.form.judulBuku)
      formData.append('kodeBuku', this.form.kodeBuku)
      formData.append('penerbit', this.form.penerbit)
      formData.append('pengarang', this.form.pengarang)
      formData.append('tahunTerbit', this.form.tahunTerbit)
      formData.append('hargaBuku', this.form.hargaBuku)
      this.$axios.post('/buku/input', formData)
        .then((res) => {
          if (res.data.error) {
            this.$q.notify({
              color: 'negative',
              message: res.data.msg,
              icon: 'ion-close'
            })
          } else {
            this.$q.notify({
              color: 'positive',
              message: res.data.msg,
              icon: 'ion-close'
            })
            this.$router.push('/')
          }
        })
    }
  }
}
</script>

<style scoped>

</style>
