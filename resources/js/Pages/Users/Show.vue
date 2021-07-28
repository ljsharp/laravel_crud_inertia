<template>
    <app-layout title="Dashboard">
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Show
            </h2>
        </template>

        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="p-5 overflow-hidden bg-white shadow-md sm:rounded-lg">
                  Name: {{ user.name }} <br/>
                  Role: {{ user.role }} <br/>
                  Email: {{ user.email }} <br/>
                  Created at: {{ user.created_at }} <br/>
                  Updated at: {{ user.updated_at }}
                </div>
            </div>
        </div>
    </app-layout>
</template>

<script>
    import AppLayout from '@/Layouts/AppLayout.vue'

    export default {
        components: {
            AppLayout,
        },
        props: ['user']
    }
</script>
