<script>
import {mapState} from 'vuex'
import {loginUrl, userUrl, getheader} from './../config';
import {clientId, clientSecret} from './../env';


export default {
    data() {
        return {
            login: {
                email: 'dima.krol@mail.ru',
                password: '123123'
            }
        }
    },
    methods: {
        handleLoginFormSubmit() {
            const postData = {
                grant_type: 'password',
                client_id: clientId,
                client_secret: clientSecret,
                username: this.login.email,
                password: this.login.password,
                scope: ''
            };

            const authUser = {};

            this.$http.post(loginUrl,postData)
                    .then(response => {
                        if (response.status == 200) {
                            console.log('Oauth token', response);

                            authUser.access_token = response.data.access_token;
                            authUser.refresh_token = response.data.refresh_token;
                            window.localStorage.setItem('authUser', JSON.stringify(authUser));

                            this.$http.get(userUrl, {headers: getheader()})
                                    .then(response => {
                                        console.log('User Object', response);

                                        authUser.email = response.body.email;
                                        authUser.name  = response.body.name;
                                        window.localStorage.setItem('authUser', JSON.stringify(authUser));
                                        this.$store.dispatch('setUserObject', authUser)
                                        this.$router.push({name: 'dashboard'})
                                    })
                        }
                    })
        }
    },
    computed: {
      ...mapState({
        userStore: state => state.userStore
      })
    }
}
</script>

<template>
    <div class="wrapper" id="login-wrapper">
        <section class="login">
            <div class="row">
                <div class="col-md-6 col-md-push-3">
                    <div class="panel panel-default">
                        <div class="panel-heading"><strong>Login</strong></div>
                        <div class="panel-body">
                            <form v-on:submit.prevent="handleLoginFormSubmit()">
                                <div class="form-group">
                                    <label>Email address</label>
                                    <input
                                            class="form-control"
                                            placeholder="Enter your email address"
                                            type="text"
                                            v-model="login.email"
                                    >
                                </div>
                                <div class="form-group">
                                    <label>password</label>
                                    <input
                                            class="form-control"
                                            placeholder="Enter your password"
                                            type="text"
                                            v-model="login.password"
                                    >
                                </div>
                                <button class="btn btn-primary">Login</button>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>

