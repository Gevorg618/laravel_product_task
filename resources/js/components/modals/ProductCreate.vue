<template>
    <div>
        <button type="button" class="btn btn-outline-primary" data-bs-toggle="modal" data-bs-target="#productCreateModal">
            Add Product
        </button>

        <!-- Modal -->
        <div class="modal fade" id="productCreateModal" tabindex="-1" aria-labelledby="productCreateModalLabel" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="productCreateModalLabel">Create Product</h5>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                        <div class="row">
                            <label for="inputName" class="col-sm-2 col-form-label">Name</label>
                            <div class="col-sm-10">
                                <input v-model="productData.name" type="text" class="form-control" id="inputName">
                            </div>
                        </div>
                    </div>
                    <div class="modal-footer">
                        <button ref="closeBtn" type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                        <button @click="save" type="button" class="btn btn-primary">Create</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "ProductCreate",
    data() {
        return {
            productData: {
                name: ''
            }
        }
    },
    methods: {
        async save() {
            let response = await this.$store.dispatch('store', this.productData)
            if (response) {
                Vue.swal({
                    position: 'top-end',
                    icon: 'success',
                    title: 'Created',
                    showConfirmButton: false,
                    timer: 1500
                });
                this.$refs.closeBtn.click()
            }
        }
    }
}
</script>
