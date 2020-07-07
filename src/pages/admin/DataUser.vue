<template>
  <q-page padding>
    <div class="row q-md-md col-gutter-md">
      <div class="col-md-12 col-xs-12 col-lg-12">
      <div class="row">
        <div class="col-auto">
          <div class="left blue"></div>
        </div>
        <div class="col">
          <q-banner inline-actions class="text-blue-gray-14">
            <div class="text-h6">Data User</div>
            <div>Data Pelanggan Anda</div>
          </q-banner>
        </div>
      </div>
      </div>
    </div>
    <q-card flat>
      <q-table
        :data="data"
        flat
        :columns="columns"
        row-key="name"
      >
        <template v-slot:body="props">
          <q-tr :props="props">
            <q-td key="username" :props="props">
              {{ props.row.username }}
            </q-td>
            <q-td key="namaLengkap" :props="props">
              {{ props.row.namaLengkap }}
            </q-td>
            <q-td key="email" :props="props">
              {{ props.row.email }}
            </q-td>
          </q-tr>
        </template>
      </q-table>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      columns: [
        { name: 'username', align: 'center', label: 'Username', field: 'username', sortable: true },
        { name: 'namaLengkap', align: 'center', label: 'Nama Lengkap', field: 'namaLengkap', sortable: true },
        { name: 'email', align: 'center', label: 'E-mail', field: 'email' }
      ],
      data: []
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.$axios.get('user/getalluser')
        .then(res => {
          if (res.data.sukses) {
            this.data = res.data.data
          } else {
            this.$showNotif(res.data.pesan, 'negative')
          }
        })
    }
  }
}
</script>
<style scoped>
.left {
  width: 3px;
  height: 100%;
  background-color: rgb(49, 245, 245);
}
</style>
