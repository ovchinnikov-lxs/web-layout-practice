<template>
    <div class="DefaultLayout">
        <TheHeader class="header"/>

        <div class="page">
            <slot />
        </div>
    </div>
</template>

<style lang="scss" scoped>
.DefaultLayout {
    position: relative;
    display: flex;
    flex-direction: column;
    width: 100%;
    height: 100%;
    min-height: 100vh;
}

.header {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 2;
    pointer-events: none;
}

.page {
    position: relative;
    z-index: 1;
}
</style>
