<template>
    <div class="container mt-5">
        <div class="row justify-content-center">
            <div class="col-12 col-md-6">
                <div>
                    <div class="row mb-3">
                        <label for="inputEmail3" class="col-sm-2 col-form-label">Email</label>
                        <div class="col-sm-10">
                            <input v-model="loginData.email" type="email" class="form-control" id="inputEmail3">
                        </div>
                    </div>
                    <div class="row mb-3">
                        <label for="inputPassword3" class="col-sm-2 col-form-label">Password</label>
                        <div class="col-sm-10">
                            <input v-model="loginData.password" type="password" class="form-control" id="inputPassword3">
                        </div>
                    </div>
                    <button @click="login" class="btn btn-primary">Sign in</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Login",
    data() {
        return {
            loginData: {
                email: '',
                password: ''
            }
        }
    },
    methods: {
        async login() {
            let {data} = await this.$store.dispatch('login', this.loginData)
            if (data) this.$router.push({name: 'home'})
        }
    }
}
</script>
