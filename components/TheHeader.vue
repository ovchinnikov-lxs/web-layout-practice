<script setup lang="ts">
const isOpened = ref(false);
const isActive = ref(false);

let lastKeyPressTime = 0;

onMounted(() => {
    document.addEventListener('keydown', event => {
        if (event.key === ' ' || event.keyCode === 32) {
            const currentTime = new Date().getTime();
            if (currentTime - lastKeyPressTime < 300) {
                isOpened.value = !isOpened.value;
            }
            lastKeyPressTime = currentTime;
        }
    });
});

</script>

<template>
    <div class="TheHeader">
        <transition name="bottom" mode="out-in">
            <div v-if="isOpened" class="wrapper">

                <div
                    class="hum"
                    tabindex="0"
                    role="button"
                    @click="isActive = !isActive"
                >
                    <span></span>
                    <span></span>
                    <span></span>
                </div>

                <transition name="right" mode="out-in">
                    <nav v-if="isActive" class="nav">
                        <NuxtLink to="/parallax-3d" class="link">parallax-3d</NuxtLink>
                        <NuxtLink to="/draggable-page" class="link">draggable-page</NuxtLink>
                    </nav>
                </transition>
            </div>
        </transition>
    </div>
</template>


<style scoped lang="scss">
.wrapper {
    display: flex;
    align-items: flex-start;
    column-gap: calc(var(--ui-unit) * 8);
    padding: calc(var(--ui-unit) * 4);
}

.hum {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    width: calc(var(--ui-col) * 2);
    height: calc(var(--ui-col) * 2);
    row-gap: calc(var(--ui-unit) * 2);
    border-radius: 50%;
    border: 3px solid var(--ui-white-color);
    background-color: var(--ui-secondary-color);
    outline: none;
    pointer-events: auto;
    transition: all .3s ease;
    cursor: pointer;

    @include hover {
        background-color: var(--ui-secondary-color);
        opacity: .64;
    }

    span {
        display: block;
        width: calc(var(--ui-unit) * 8);
        height: 2px;
        background-color: var(--ui-white-color);
    }
}

.nav {
    display: flex;
    flex-wrap: wrap;
    column-gap: calc(var(--ui-unit) * 3);
    row-gap: calc(var(--ui-unit) * 3);
    padding: calc(var(--ui-unit) * 4);
    border-radius: calc(var(--ui-unit) * 16);
    border: 3px solid var(--ui-white-color);
    background: var(--ui-secondary-color);
    pointer-events: auto;
}

.link {
    padding: calc(var(--ui-unit) * 4);
    border-radius: calc(var(--ui-unit) * 8);
    background-color: rgba(#fff, .4);
    color: var(--ui-white-color);
    transition: color .3s ease, background-color .3s ease;

    @include hover {
        background-color: var(--ui-white-color);
        color: var(--ui-secondary-color);
    }
}

// In css modules looks pretty better
:global(.link.--is-exact-link) {
    background-color: rgba(#fff, .8);
    color: var(--ui-secondary-color);
}
</style>
