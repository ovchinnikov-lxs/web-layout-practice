<script setup lang="ts">
// UiKit Components
import { UiImage, UiButton } from '@ovchinnikov-lxs-frontend/ui-kit';

const movePosition = reactive({
    x: 0,
    y: 0,
});
const styleList = computed(() => [{
    '--move-x': `${movePosition.x}deg`,
    '--move-y': `${movePosition.y}deg`,
}]);


function addListeners() {
    document.addEventListener('mousemove', e => {
        movePosition.x = (e.clientX - window.innerWidth / 2) * -0.005;
        movePosition.y = (e.clientY - window.innerHeight / 2) * -0.01;
    });
}

onMounted(() => {
    addListeners();
});
</script>

<template>
    <section class="Parallax-3d">
        <div :style="styleList" class="wrapper">
            <div class="container">
                <UiImage origin="/web-layout-practice/parallax-3d/layer-1.webp" class="item layer-1"/>
                <UiImage origin="/web-layout-practice/parallax-3d/layer-2.webp" class="item layer-2"/>
                <div class="item layer-3">
                    <div class="content">
                        <h1 class="title">
                            Some Title
                        </h1>

                        <p class="text">Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>

                        <UiButton
                            rounded
                            outline
                            size="large"
                            class="button"
                        >
                            Button title
                        </UiButton>
                    </div>
                </div>
                <UiImage origin="/web-layout-practice/parallax-3d/layer-5.webp" class="item layer-5"/>
                <UiImage origin="/web-layout-practice/parallax-3d/layer-6.webp" class="item layer-6"/>
            </div>
        </div>
    </section>
</template>

<style lang="scss" scoped>
.Parallax-3d {
    background-color: var(--ui-black-color);
    color: var(--ui-white-color);
}

.wrapper {
    --index: calc(1vw + 1vh);
    --transition: 1.5s cubic-bezier(.05, .5, 0, 1);

    overflow: hidden;
    perspective: 1000px;
}

.container {
    height: 100vh;
    transform: rotateX(var(--move-y)) rotateY(var(--move-x));
    transition: transform var(--transition);
    transform-style: preserve-3d;
    will-change: transform;
}

.item {
    position: absolute;
    inset: -10vw;
    pointer-events: none;

    img {
        user-select: none;
    }
}

.layer-1 {
    transform: translateZ(-80px) scaleX(1.06);
}

.layer-2 {
    transform: translateZ(80px) scaleX(.88);
}

.layer-3 {
    display: flex;
    align-items: center;
    justify-content: center;
    transform: translateZ(180px) scaleX(.88);
}

.content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    pointer-events: auto;
}

.title {
    text-transform: uppercase;
    font-size: calc(var(--index) * 6);
    font-weight: bold;
}

.text {
    font-size: calc(var(--index) * .5);
}

.button {
    margin-top: calc(var(--ui-unit) * 8);

    &:global(.UiButton) {
        &:global(.--is-outline) {
            border-style: solid;
        }

        &:global(.--is-rounded) {
            border-radius: calc(var(--ui-unit) * 12);
        }

        &:global(.--large-size) {
            &:global(.--is-outline) {
                padding: calc(var(--ui-unit) * 3) calc(var(--ui-unit) * 12);
                border-width: calc(var(--ui-unit) / 2);
            }
        }

        &:global(.--main-color) {
            border-color: var(--ui-white-color);
            background-color: transparent;
            color: var(--ui-white-color);
        }
    }

    @include hover {
        background-color: var(--ui-secondary-color);
    }
}

.layer-5 {
    transform: translateZ(300px) scaleX(.9);
}

.layer-6 {
    transform: translateZ(380px);
}
</style>
