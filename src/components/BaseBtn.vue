<template>
<a class="btn" @click="$play(url)">
    {{ name }}
</a>
</template>

<script>
export default {
    name: "BaseButton",
    props: ["url", "btnName"],
    computed: {
        name() {
            try {
                return this.$loc(this.btnName)
            } catch (e) {
                console.log(e.message, this.btnName, this.url)
                return null
            }
        }
    }
}
</script>

<style>
.btn {
    /*   Neuromophism design   */
    border-radius: 16px;
    background: var(--btn-color);
    box-shadow: var(--box-shadow);
    /* Neuromophism design ends*/
    padding: 1em;
    height: 1.2em;
    min-width: 5rem;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: all 0.1s ease;
    margin: 0.8em;
    font-size: 1rem;
    cursor: pointer;
}

.btn:active {
    transform: scale(1.05, 1.05);
}

.btn:hover {
    box-shadow: var(--hover-shadow)
}
</style>
