<template>
    <div>
        <div v-if="isAvailable" class="container">
            <div class="row">
                <div class="col-md-4">
                    <div class="nav flex-column nav-pills me-3" id="v-pills-tab" role="tablist"
                         aria-orientation="vertical">
                        <button class="nav-link active mt-3" id="v-pills-home-tab" data-bs-toggle="pill"
                                data-bs-target="#v-pills-home" type="button" role="tab" aria-controls="v-pills-home"
                                aria-selected="true">Messages
                        </button>
                        <button class="nav-link mt-3" id="v-pills-profile-tab" data-bs-toggle="pill"
                                data-bs-target="#v-pills-profile" type="button" role="tab"
                                aria-controls="v-pills-profile" aria-selected="false">News
                        </button>
                        <button class="nav-link mt-3" id="v-pills-settings-tab" data-bs-toggle="pill"
                                data-bs-target="#v-pills-settings" type="button" role="tab"
                                aria-controls="v-pills-settings" aria-selected="false"> Products
                        </button>
                        <button class="nav-link mt-3 mb-5" id="v-pills-products-tab" data-bs-toggle="pill"
                                data-bs-target="#v-pills-products" type="button" role="tab"
                                aria-controls="v-pills-settings" aria-selected="false">Categories
                        </button>
                    </div>
                </div>
                <div class="col-md-8">
                    <div class="tab-content" id="v-pills-tabContent">
                        <div class="tab-pane fade show active" id="v-pills-home" role="tabpanel"
                             aria-labelledby="v-pills-home-tab">
                            <v-messages></v-messages>
                        </div>
                        <div class="tab-pane fade" id="v-pills-profile" role="tabpanel"
                             aria-labelledby="v-pills-profile-tab">
                            <v-adminNews></v-adminNews>
                        </div>
                        <div class="tab-pane fade" id="v-pills-settings" role="tabpanel"
                             aria-labelledby="v-pills-settings-tab">
                            <v-adminProducts></v-adminProducts>
                        </div>
                        <div class="tab-pane fade" id="v-pills-products" role="tabpanel"
                             aria-labelledby="v-pills-products-tab">
                            <v-categoryManage></v-categoryManage>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import authService from "../../services/authService";

export default {
    name: "AdminPanel",
    data() {
        return {
            isAvailable: false
        }
    },
    created() {
        this.getUserStatus()
    },
    methods: {
        getUserStatus() {
            authService.getUserStatus().then(response => {
                if (response.data === 'admin') {
                    this.isAvailable = true
                } else {
                    window.location.replace('/');
                }
            })
                .catch(error => console.log(error))
                .finally()
        }
    }
}
</script>

<style scoped>

.nav-link:hover {
    color: #942c34;
    border-bottom: 1px dotted #942c34;
}

.nav-link {
    background-color: #010302;
    border-bottom: 1px dotted #ffffff;
    color: #fa4251;
}

.nav-pills .nav-link.active, .nav-pills .show > .nav-link {
    background-color: #010302;
    border-bottom: 1px dotted #942c34;
    color: #942c34
}

</style>
