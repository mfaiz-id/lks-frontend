<template>
    <div class="card" style="width: 18rem;">
        <div class="card-body">
            <h5 class="card-title">{{barangnya.nama_barang}}</h5>
            <table border="0" width="100%" cellpadding="10" cellspacing="0">
                <tr>
                    <th align="left">Harga</th>
                    <td>:</td>
                    <td>{{barangnya.harga}}</td>
                </tr>
                <tr>
                    <th align="left">Stok</th>
                    <td>:</td>
                    <td>{{barangnya.stok}}</td>
                </tr>
            </table>
           <button type="button" class="btn btn-sm btn-primary">Detail</button> &nbsp;
           <button type="button" class="btn btn-sm btn-warning" @click="editData">Edit</button> &nbsp;
           <button type="button" class="btn btn-sm btn-danger">Hapus</button> &nbsp;
        </div>
    </div>
</template>
<script>
export default {
    name:'CardBarang',
    props:{
        barangnya:{
            type:Object,
            required:true
        }
    },
    methods:{
        editData(){
            this.$emit('ceeditbarang', this.barangnya)
        }
    }
}
</script>