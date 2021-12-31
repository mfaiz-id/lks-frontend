<template>
    <div>
        <h3>Barang</h3>
        <div class="row">
            <div class="col-md" v-for="(brg,index) in dataBarang" :key="index">
                <card-barang :barangnya="brg" ></card-barang>
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
            dataBarang:[]
        }
    },
    methods:{
        loadData(){
           axios.get(`http://127.0.0.1:8000/api/barang`)
            .then(response => {
                this.dataBarang = response.data
            })
            .catch(error => {
                console.error(error);
            })
        }, 
    }
}
</script>