<template>
    <div class="container d-flex justify-content-center p-4">
        <form class="row row-cols-lg-auto g-3 align-items-center" @submit.prevent="searchCharacters">
            <div class="col-12">
                <label class="visually-hidden" for="charactername">Search name</label>
                <input type="text" class="form-control" id="charactername" placeholder="Search name"
                    v-model.trim="store.searchName">
            </div>

            <div class="col-12">
                <label class="visually-hidden" for="searchStatus">Search status</label>
                <select class="form-select" id="searchStatus" v-model="store.searchStatus">
                    <option selected value="">Choose...</option>
                    <option :value="status" v-for="(status, index) in statusOptions" :key="index">{{ status }}</option>

                </select>
            </div>

            <div class="col-12">
                <button type="submit" class="btn btn-primary">Search</button>
            </div>

            <div class="col-12">
                <button type="reset" class="btn btn-primary" @click="resetSearch">Reset</button>
            </div>
        </form>
    </div>

</template>

<script>
import { store } from '../store';
export default {
    name: 'AppSearch',
    data() {
        return {
            store,
            statusOptions: [
                'alive',
                'dead',
                'unknown'
            ],
            search: ''
        }
    },
    // props: {
    //     searchStatus: String
    // },
    methods: {
        searchCharacters() {
            this.$emit('filterChar');
        },
        resetSearch() {
            store.searchStatus = '';
            store.searchName = '';
            this.$emit('filterChar')
        }
    }
}
</script>

<style lang="scss" scoped>

</style>