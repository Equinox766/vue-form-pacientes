<script setup>
    import { computed } from 'vue';
    const props = defineProps({
        alert: {
            type: Object,
            required: true
        },
    })
    const isError = computed(() => {
        return props.alert.type === 'error'
    })
</script>

<template>
    <div :class="[isError ? 'bg-red-500' : 'bg-green-500']" class="text-white text-center p-3 uppercase font-bold rounded-md">
        {{ alert.msg }}
    </div>
</template>