<template>
<div class="color-card" :style="style" @click="$store.commit('changeColor', cid)">
    <div class="demo-cat">{{ $t("demo_cat") }}</div>
    <div class="demo-btn">{{ $t("demo_btn") }} 1</div>
    <div class="demo-btn">{{ $t("demo_btn") }} 2</div>
    <a class="pallet-name">{{ $loc(color.name) }}</a>
</div>
</template>

<script>
export default {
    props: ["cid", "color"],
    computed: {
        boxShadow: function () {
            const bs = this.color.boxShadow; // Box Shadow
            const i = this.color.distance || 10; // distance
            const b = this.color.blur || 2 * i; // blur
            return `${i}px ${i}px ${b}px ${bs[0]}, -${i}px -${i}px ${b}px ${bs[1]}`
        },
        style: function () {
            return {
                '--demo-box-shadow': this.boxShadow,
                '--demo-font-color': this.color.fontColor,
                '--demo-background': this.color.background,
                '--demo-btn-color': this.color.btnColor,
                '--demo-btn-font-color': this.color.btnFontColor
            }
        },
        isPrime: function () {
            return this.$colorChoice == this.cid
        }
    }
}
</script>

<style>
.color-card {
    position: relative;
    width: 15rem;
    height: 20rem;
    box-shadow: var(--box-shadow);
    color: var(--demo-btn-font-color);
    background: var(--demo-background);
    margin: 1rem;
    padding: 2rem;
    border-radius: 16px;
    box-sizing: border-box;
    cursor: pointer;
}

.demo-cat {
    margin-right: 4px;
    font-size: 1.5em;
    color: var(--demo-font-color);
}

.demo-btn {
    box-shadow: var(--demo-box-shadow);
    color: var(--demo-btn-font-color);
    background: var(--demo-btn-color);
    padding: 1rem;
    border-radius: 16px;
    box-sizing: border-box;
    margin: 1rem 0;
}

.pallet-name {
    position: absolute;
    right: 1rem;
    bottom: 1rem;
    color: var(--demo-font-color);
}
</style>
