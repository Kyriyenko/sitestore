<template>
    <div>
        <div v-if="isUpdated" class="alert alert-success" role="alert">
            {{serverMessage}}
        </div>
        <ul class="nav nav-tabs mb-3" id="myTab" role="tablist">
            <li class="nav-item" role="presentation">
                <button class="nav-link active" id="home-tab" data-bs-toggle="tab" data-bs-target="#home" type="button"
                        role="tab" aria-controls="home" aria-selected="true">All products
                </button>
            </li>
            <li class="nav-item" role="presentation">
                <button class="nav-link" id="profile-tab" data-bs-toggle="tab" data-bs-target="#profile" type="button"
                        role="tab" aria-controls="profile" aria-selected="false">Create product
                </button>
            </li>
        </ul>
        <div class="tab-content" id="myTabContent">
            <div class="tab-pane fade show active" id="home" role="tabpanel" aria-labelledby="home-tab">
                <div class="container">
                    <div class="row">
                        <div class="col">
                            <div class="row content">
                                <div v-for="product in products" class="col mt-2 mb-2">
                                    <div class="product-item">
                                        <div class="mt-2">TITLE</div>
                                        <input class="mt-2" type="text" v-model="product.title">
                                        <div class="mt-2">DESCRIPTION</div>
                                        <input class="mt-2" type="text" v-model="product.description">
                                        <div class="mt-2">PRICE</div>
                                        <input class="mt-2" type="text" v-model="product.price">
                                        <div class="btn-box mt-3">
                                            <button type="button" class="btn btn-success"
                                                    v-on:click="updateProductInfo(product)">SAVE CHANGES
                                            </button>
                                            <button type="button" class="btn btn-delete"
                                                    v-on:click="deleteProduct(product.id)">DELETE
                                            </button>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="tab-pane fade" id="profile" role="tabpanel" aria-labelledby="profile-tab">
                <v-creationProduct></v-creationProduct>
            </div>
        </div>
    </div>
</template>

<script>
import adminService from "../../services/adminService";

export default {
    name: "Products",
    data() {
        return {
            products: [],
            category: '',
            categories: [],
            isDeletedMode: false,
            serverMessage:'',
            isUpdated:false,
        }
    },
    created() {
        this.getAllProducts()
    },
    methods: {
        updateProductInfo(product) {
            this.isUpdated=false
            adminService.updateProductInfo(product).then(response => {
                if (response.data.status === true) {
                    this.isUpdated=true
                    this.serverMessage=response.data.message
                    this.getAllProducts()
                }
            })
                .catch(error => console.log(error))
                .finally()
        },
        deleteProduct(id) {
            adminService.deleteProduct({id: id}).then(response => {
                if (response.data.success === true) {
                    this.getAllProducts()
                }
            })
                .catch(error => console.log(error))
                .finally()
        },
        getAllProducts() {
            adminService.getAllProductsForUpdate().then(response => {
                this.products = response.data
            })
                .catch(error => console.log(error))
                .finally()
        },
    }
}
</script>

<style scoped>

.row {
    display: flex;
}

.product-item {
    border: 1px solid #ffffff;
    padding: 10px;
}

h4 {
    text-transform: uppercase;
}

input {
    background-color: #000000;
}

ul {
    border: 1px solid #ffffff;
    background-color: #000000;
}

.nav-link {
    color: #ffffff;
}

.btn-delete{
    background-color: #424242;
    color: #ffffff;
}

</style>
