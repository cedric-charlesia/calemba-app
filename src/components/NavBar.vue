<script setup>
import MenuItem from './MenuItem.vue';
</script>

<template>
    <MenuItem>

    <!-- Logo -->
    <template #app-logo>
        <a href="/">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="text-sky-700 h-8 w-8 md:h-10 md:w-10"><path stroke-linecap="round" stroke-linejoin="round" d="M14.25 7.756a4.5 4.5 0 100 8.488M7.5 10.5h5.25m-5.25 3h5.25M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
        </a>
    </template>

    <template #app-name>
        <a href="/">
            <span class="text-sky-700 text-lg">Calemba</span>
        </a>
    </template>

    <!-- Desktop Menu -->
    <template #menu-link>
        <a href="https://github.com/cedric-charlesia/calemba-app" target="_blank" class="hover:text-sky-600">Code Source</a>
        <a href="https://cedriccharlesia.com/" class="hover:text-sky-600">Retour au portfolio</a>
    </template>

    <!-- Mobile Burger Menu -->

    <template #burger-button>
        <button type="button" class="text-sky-700">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
                class="w-8 h-8">
                <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
            </svg>

        </button>
    </template>

    <!-- Mobile Menu -->
    <template #mobile-menu-link>
        <a href="https://github.com/cedric-charlesia/calemba-app" target="_blank" class="hover:text-sky-600">Code Source</a>
        <a href="https://cedriccharlesia.com/" class="hover:text-sky-600">Retour au portfolio</a>
    </template>

    </MenuItem>
</template>