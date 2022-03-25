<template>
    <div class="container mt-5">
        <div class="row justify-content-center">
            <div class="col-6">
                <div v-if="product">
                    <label for="inputName" class="col-sm-2 col-form-label">Name</label>
                    <div>
                        <input v-model="product.name" type="text" class="form-control" id="inputName">
                    </div>
                    <div class="mt-3 d-flex justify-content-end">
                        <button @click="update" class="btn btn-primary">Save</button>
                    </div>
                </div>
                <div v-else>
                    <h2 class="text-center">Product not found</h2>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Product",
    computed: {
        product() {
            return this.$store.getters.GET_PRODUCT
        }
    },
    methods: {
        async update() {
            let response = await this.$store.dispatch('update', this.product)
            if (response) Vue.swal({
                position: 'top-end',
                icon: 'success',
                title: 'Edited',
                showConfirmButton: false,
                timer: 1500
            });
        }
    },
    beforeCreate() {
        this.$store.dispatch('show', this.$route.params.id)
    }
}
</script>
