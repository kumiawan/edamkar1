<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import Map from '@/Components/Map.vue';
import { Head } from '@inertiajs/vue3';
</script>

<template>

    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="underline underline-offset-8 decoration-c text-3xl font-semibold leading-tight text-white">
                Pemantauan</h2>
                <div class="inline-flex w-64 h-12 bg-b text-white text-medium text-xl items-center justify-center rounded-xl">Posko Kota Jember</div>
        </template>

    <div class="grid grid-cols-4 gap-4"> 
        <div class="h-80 col-span-3 bg-d"> 
            <Map></Map>
        </div>
        <div class="bg-d">cuaca</div>
        <div class="h-96 col-span-3 bg-d">1</div>
        <div class="bg-d">status tim</div>
    </div>
    </AuthenticatedLayout>

</template>
