<template>
    <div class="container">
        <div v-if="loading2">
            Sto Caricando
        </div>
        <div class="row" v-if="!loading2">
            <div class="col-12 col-sm-6 col-md-4 col-lg-3" v-for="(item, index) in characters" :key="item.id">
                <CardComponent :character="item" />
            </div>
        </div>
    </div>

</template>

<script>
import CardComponent from './CardComponent.vue';

export default {
    name: "CharacterList",
    props: ["characters", "loading2"],
    components: { CardComponent }
}
</script>

<style lang="scss" scoped>

</style>