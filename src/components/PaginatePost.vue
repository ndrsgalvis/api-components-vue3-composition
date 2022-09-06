<script setup>

    defineProps({
        start: Number, 
        end: Number,
        maxLength: Number,
    })
    const emit = defineEmits(["next", "before"]);
</script>
<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button  
         @click="emit('before')" 
         type="button" 
         class="btn btn-outline-primary"
         :disabled="start <= 0">
            Anterior {{start}}
        </button>
        <button  
         @click="emit('next')" 
         type="button" 
         class="btn btn-outline-primary"
         :disabled="end >= maxLength">
            Siguiente {{end}}
        </button>
    </div>
</template>