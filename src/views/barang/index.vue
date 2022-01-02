<template>
    <div>
        <h3>Barang</h3>
        <div class="row">
            <div class="col-md-12">
                <button class="btn btn-sm btn-success" @click="showFormTambah">
                    + Tambah
                </button>
            </div>
        </div>
        <br>
        <div class="row" v-show="showForm">
            <div class="col-md-4">
                <input type="text" v-model="namaBarang" placeholder="Silakan input nama barang ...">
                <br>
                <input type="number" v-model="stokBarang" placeholder="Silakan stok  barang ...">
                <br>
                <input type="number" v-model="hargaBarang" placeholder="Silakan harga barang ...">
                <br>
                <button type="button" @click="simpan">Simpan</button>
                <button type="button" @click="hideFormBarang">Batal</button>
                <p v-show="loading">Loading....</p>
                <br>
            </div>
        </div>
        <br>
        <div class="row">
            <div class="col-md-3" v-for="(brg,index) in dataBarang" :key="index">
                <card-barang :barangnya="brg" @ceeditbarang="showFormEdit" ></card-barang>
            </div>
        </div>
    </div>
</template>
<script>
import CardBarang from '@/components/barang/CardBarang.vue'
import axios from 'axios'
export default {
    components:{
        'card-barang':CardBarang
    },
    created(){
        this.loadData()
    },
    data(){
        return {
            loading: false,

            dataBarang:[],
            showForm:false,
            modeForm:'tambah',

            namaBarang:'',
            stokBarang:'',
            hargaBarang:'',
            idBarang:'',
        }
    },
    methods:{
        loadData(){
           axios.get(`http://127.0.0.1:8000/api/barang`)
            .then(response => {
                if(response.data.sukses==true){
                    this.dataBarang = response.data.barang
                }
            })
            .catch(error => {
                console.error(error);
            })
        }, 
        showFormTambah(){
            this.showForm = true
            this.modeForm = 'tambah'
        },
        hideFormBarang(){
            this.showForm = false
            this.namaBarang=''
            this.stokBarang=''
            this.hargaBarang=''
        },
        simpan(){
            this.loading = true
            if(this.modeForm=='tambah'){
                this.prosesTambah()
            }else if(this.modeForm=='edit'){
                this.prosesEdit()
            }
        },
        prosesTambah(){
            axios.post('http://127.0.0.1:8000/api/barang',
            { 
                nama_barang: this.namaBarang,
                stok: this.stokBarang,
                harga: this.hargaBarang
            })
            .finally( ()=> {
                setTimeout(() => {
                    this.loading=false
                }, 1000);
            })
            .then((result)=>{
                if(result.data.success==true){
                    setTimeout(() => {
                        this.loading=false
                        this.loadData()
                        this.hideFormBarang()
                    }, 1000);
                }
            })
            .catch((err)=>console.log('error', err))
        },
        prosesEdit(){
            axios.put('http://127.0.0.1:8000/api/barang',
            { 
                nama_barang: this.namaBarang,
                stok: this.stokBarang,
                harga: this.hargaBarang,
                id: this.idBarang
            })
            .finally( ()=> {
                setTimeout(() => {
                    this.loading=false
                }, 1000);
            })
            .then((result)=>{
                if(result.data.success==true){
                    setTimeout(() => {
                        this.loading=false
                        this.loadData()
                        this.hideFormBarang()
                    }, 1000);
                }
            })
            .catch((err)=>console.log('error', err))
        },
        showFormEdit(barangnya){
            // console.log('barangnya', barangnya)
            this.showForm=true
            this.modeForm = 'edit'
            this.namaBarang=barangnya.nama_barang
            this.stokBarang=barangnya.stok
            this.hargaBarang=barangnya.harga
            this.idBarang=barangnya.id
        }
    }
}
</script>