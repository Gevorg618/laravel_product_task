<template>
    <div class="container mt-5">
        <div class="row">
            <div class="col-12">
                <ProductCreate/>
            </div>
            <div class="col-12 mt-4">
                <div class="input-group mb-3">
                    <input type="text" v-model="searchQuery" placeholder="Search" class="form-control">
                    <button @click="getProducts" class="input-group-text">Search</button>
                </div>

            </div>
            <template v-if="products.length">
                <div v-for="product in products" class="col-12 col-md-6 col-lg-3 mt-3">
                    <div class="card">
                        <button @click="destroy(product.id)" class="btn btn-danger remove">
                            <Trash color="white"/>
                        </button>
                        <div class="card-body">
                            <small>Product Name:</small><h5 class="card-title"><b>{{ product.name }}</b></h5>
                            <p class="card-text">Author Name: {{product.author_name}}</p>
                            <router-link
                                :to="{
                                name: 'product',
                                 params: {
                                    id: product.id
                                }}"
                                class="btn btn-primary">
                                Edit
                            </router-link>
                        </div>
                    </div>
                </div>
            </template>
            <div v-else class="mt-4">
                <p class="text-center">No Data</p>
            </div>
            <div v-if="meta.last_page > 1" class="col-12 mt-4">
                <nav aria-label="Page navigation example">
                    <ul class="pagination">
                        <li v-for="page in meta.last_page"
                            :class="page == selectedPage && 'active'"
                            class="page-item">
                            <a role="button" @click="getProducts(page)" class="page-link">{{ page }}</a>
                        </li>
                    </ul>
                </nav>
            </div>
        </div>
    </div>
</template>

<script>
import ProductCreate from "../components/modals/ProductCreate";
import Trash from "../components/icons/Trash";

export default {
    name: "Home",
    components: {
        ProductCreate,
        Trash
    },
    data() {
        return {
            selectedPage: 1,
            searchQuery: ''
        }
    },
    computed: {
        products() {
            return this.$store.getters.GET_PRODUCTS
        },
        meta() {
            return this.$store.getters.GET_META
        }
    },
    methods: {
        getProducts(page = 1) {
            this.selectedPage = page
            this.$store.dispatch('getProducts', {
                params: {
                    page: this.selectedPage,
                    search: this.searchQuery
                }
            })
        },
        destroy(id) {
            this.$store.dispatch('destroy', id)
        }
    },
    created() {
        this.getProducts()
    }
}
</script>

<style lang="scss" scoped>
.card {
    &:hover {
        .remove {
            display: block;
        }
    }

    .remove {
        position: absolute;
        display: none;
        right: 0;
        top: 0
    }
}
</style>
