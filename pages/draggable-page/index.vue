<script setup lang="ts">
// UiKit Components
import { UiImage } from '@ovchinnikov-lxs-frontend/ui-kit';

import { gsap } from 'gsap';
import { Draggable } from 'gsap/Draggable';

gsap.registerPlugin(Draggable);

useSeoMeta({
    title: 'Draggable Page',
});

const isLoading = ref(true);
const galleryItem = Array
    .from({ length: 19 }, (_, index: number): string => `/web-layout-practice/draggable-page/${index + 1}.webp`);

const masonryGrid = [
    ...galleryItem,
    ...galleryItem,
    ...galleryItem,
    ...galleryItem,
];

const galleryRef = ref<HTMLDivElement>();

onMounted(() => {
    setTimeout(() => {
        if (!galleryRef.value) {
            return false;
        }

        Draggable.create(galleryRef.value, {
            bounds: 'body',
            inertia: true,
        });

        isLoading.value = false;
    }, 500);
});
</script>

<template>
    <section class="DraggablePage">
        <div class="wrapper">
            <transition name="fade">
                <DraggablePageLoader v-if="isLoading" class="loader"/>
                <h1 v-else class="title">Some Content</h1>
            </transition>

            <transition name="fade" mode="out-in">
                <div
                    v-show="!isLoading"
                    ref="galleryRef"
                    class="gallery"
                >
                    <div
                        v-for="item in masonryGrid"
                        :key="item"
                        class="item"
                    >
                        <UiImage
                            :origin="item"
                            :lazy="false"
                            class="image"
                        />
                    </div>
                </div>
            </transition>
        </div>
    </section>
</template>

<style scoped lang="scss">
.wrapper {
    --bg-color: var(--ui-white-color);
    --text-color: var(--ui-black-color);

    @media (prefers-color-scheme: dark) {
        --bg-color: var(--ui-black-color);
        --text-color: var(--ui-white-color);
    }

    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100vh;
    background: var(--bg-color);
    color: var(--text-color);
}

.title {
    position: absolute;
    font-family: 'Inter', sans-serif;
    font-size: calc(var(--index) * 3);
    font-weight: lighter;
    letter-spacing: .1em;
}

.loader {
    position: absolute;
    top: 50%;
    left: 50%;
    width: calc(var(--ui-col) * 2);
    transform: translate3d(-50%, -50%, 0);
}

.gallery {
    width: 30vw;
    column-gap: .5em;
    padding: .5em;
    column-width: 2em;
    transform: scale(8);
    will-change: transform;
    transition: all 1000ms cubic-bezier(.075, 1, .25, 1);
    transition-timing-function: cubic-bezier(.075, 1, .25, 1);
}

.item {
    margin-bottom: .5em;
    will-change: transform;
    transition: transform .3s ease-in-out;

    @include hover {
        transform: scale(1.1);
    }
}

.image {
    width: 100%;
    user-select: none;
}
</style>
