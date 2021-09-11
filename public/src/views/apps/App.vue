<template lang="pug">
    div
        include ../../pug/components/phoneBook
        include ../../pug/components/login
</template>

<script>
    export default {
        data() {
            return {
                loginQ: true,
                typeLogin: "Login",
                email: "",
                password: "",
                users: "",
                data: ""
            }
        },
        methods: {
            notLogin() {
                this.loginQ = !this.loginQ
            },
            autoSign(cookie) {
                if (cookie) {
                    this.notLogin()
                }
            },
            connectingLogs() {
                if (this.typeLogin == "Sign in") {
                    for (var i = 0; i < this.users.length; i++) {
                        if (this.users[i].email == this.email && this.users[i].password == this.password) {
                            i = this.users.length
                            this.notLogin()
                        }
                    }
                }
            },
            addNew() {
                this.data[this.email].push(
                    {
                        "photo": "",
                        "name": "",
                        "desc": "",
                        "phone": ""
                    }
                )
            }
        },
        mounted() {
            fetch('../src/data/logs/data.json')
            .then(response => response.json())
            .then(json => {
                this.users = json.users
                this.data = json.data
            })
        }
    }
</script>

<style scoped></style>