<template>
<div class="home">
    <a v-if="loading">Loading</a>
    <Panel v-for="(category, index) in categories" :key='index' :clips='category.clips' :category='category.name'>
    </Panel>
</div>
</template>

<script>
import Panel from '@/components/Panel.vue'
export default {
    name: 'Home',
    components: {
        Panel
    },
    async created() {
        const loaded = (await this.$a.get(this.$store.getters.metaSource)).data
        this.categories = this.parseCategory(loaded)
    },
    data() {
        return {
            loading: true,
            categories: null
        }
    },
    methods: {
        parseCategory(loaded) {
            Object.entries(loaded.categories).forEach(([k, v]) => {
                loaded.categories[k] = {
                    name: v,
                    clips: []
                }
            })
            Object.entries(loaded.clips).forEach(([k, v]) => {
                if (typeof v.category !== 'string') v.category = v.category[0]
                v.name = v.name ?? {
                    en: k
                }
                loaded.categories[v.category].clips.push(v)
            })
            return Object.values(loaded.categories)
        }
    }
}
</script>

<style>
.home {
    display: flex;
    flex-wrap: wrap;
    width: auto;
    flex-direction: column;
}
</style>
