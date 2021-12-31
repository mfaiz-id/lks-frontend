<template>
    <div class="card" style="width: 18rem;">
        <div class="card-body">
            <h5 class="card-title">{{barangnya.nama}}</h5>
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's
                content.</p>
           <button type="button" class="btn btn-primary">Detail</button>
           <button type="button" class="btn btn-warning">Edit</button>
           <button type="button" class="btn btn-danger">Hapus</button>
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
    }
}
</script>