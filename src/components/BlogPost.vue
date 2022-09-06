<script setup>
    //defineProps(["id", "nombre" ...])

    defineProps({
        id: Number, 
        title: String, 
        colorText: String,
        body: {
            type: String,
            default: "Sin descripción"
        }, 
    });
    const emit = defineEmits(['cambiarFavorito']);
</script>
<style>
    .card{
        margin: 15px 0px;
    }
</style>
<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title"  :class="`text-${colorText}`"> {{id}} - {{title}}</h5>
            <p>{{body}}</p>
            <button
                @click = "emit('cambiarFavorito', title)"
                class="btn btn-outline-primary"> 
            Favorito </button>
        </div>
    </div>
</template>