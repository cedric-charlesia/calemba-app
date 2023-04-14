<script setup>
import { ref } from "vue";

const isOpen = ref(false);

const openMenu = () => {
    isOpen.value = !isOpen.value;
};

</script>

<template>
    <nav class="shadow-md">
            <div class="flex justify-between">

                <!-- Logo -->
                <div class="flex items-center py-2 px-2 text-gray-700 hover:text-gray-900">
                    <svg class="w-10 h-10 md:w-12 md:h-12">
                        <slot name="app-logo"></slot>
                    </svg>
                    <span class="font-bold uppercase">
                        <slot name="app-name"></slot>
                    </span>
                </div>

                <!-- Desktop Menu -->

                <div class="hidden md:flex items-center gap-4 font-bold text-gray-700 uppercase px-4">
                    <slot name="menu-link">
                        <a href="#"></a>
                        <a href="#" target="_blank"></a>
                    </slot>
                </div>

                <!-- Mobile Burger Menu -->

                <div class="md:hidden flex items-center px-2">
                    <button type="button" @click="openMenu">
                        <slot name="burger-button"></slot>
                    </button>
                </div>
            </div>

        <!-- Mobile Menu -->

        <div class="flex flex-col md:hidden gap-4 pb-4 px-4 hover:bg-gray-200 uppercase" :class="isOpen ? '' : 'hidden'">

            <slot name="mobile-menu-link">
                <a href="#"></a>
                <a href="#" target="_blank"></a>
            </slot>
        </div>
    </nav>
</template>