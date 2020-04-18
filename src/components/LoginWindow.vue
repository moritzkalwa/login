<template>
    <div class="main-container" v-if="init_done && !logged_in">
        <div class="main-window">
            <transition name="fade">
                <div id="login-window" v-if="!regstate">
                    <form class="login-form">
                        <h1>Login</h1>
                        <input type="email" id="email" name="email" v-bind:placeholder="emailplaceholder" v-model="email" /><br>
                        <input type="password" id="password" name="password" placeholder="yourpassword" v-model="password" /><br>
                            <a href="#empty">Lost your password?</a>
                    </form>
                    <button v-on:click="log">Sign in</button>
                    <button v-on:click="reg_trans">Register</button>
                </div>
            </transition>
            <transition name="fade">
                <div id="register-window" v-if="regstate">
                    <form class="register-form">
                        <h1>Register</h1>
                        <input type="email" id="email" name="email" v-bind:placeholder="emailplaceholder" v-model="email" /><br>
                        <input type="password" id="password" name="password" placeholder="yourpassword" v-model="password" /><br>
                        <label for="conf-password" v-bind:class="{ match: pass_match, dontmatch: !pass_match }">Confirm your password:</label><br>
                        <input type="password" id="conf-password" name="conf-password" placeholder="yourpassword" v-model="password_conf" /><br>
                    </form>
                    <button v-on:click="reg">Register</button>
                    <button v-on:click="reg_trans">Go back to login</button>
                </div>
            </transition>
        </div>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                email: '',
                password: '',
                password_conf: '',
                emailplaceholder: 'example@gmail.com',
                regstate: false, 
                init_done: false,
                logged_in: false
            }
        },
        methods: {
            log: function() {
                if(this.email != "") {
                    this.logged_in = true;
                    //make body scrollable
                    (document.getElementsByTagName( 'html' )[0]).removeAttribute( 'class', 'force-login' );
                } else {
                    this.emailplaceholder = "Please enter an email!";
                }
            },
            reg_trans: function() {
                this.regstate = !this.regstate;
            },
            reg: function() {

            },
            init: function() {
                var x = false;
                if(x) {
                    //user already logged in
                    this.logged_in = true;
                } else {
                    //make the body unscrollable
                    (document.getElementsByTagName( 'html' )[0]).setAttribute( 'class', 'force-login' );
                }
                this.init_done = true;
            }
        },
        created () {
            this.init();
        },
        computed: {
            pass_match: function () {
                return this.password === this. password_conf;
            }
        }
    }
</script>

<style>
    .force-login {
        overflow: hidden;
    }
    .fade-enter-active {
        transition: opacity 0.5s;
    }
    .fade-leave-active {
        transition: opacity 0.5s;
    }
    .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
        opacity: 0;
    }
    .main-container {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        min-width: 100%;
        min-height: 100%;
        background: rgba(0, 0, 255, 0.5);
    }
    .main-window {
        box-shadow: 4px 4px rgba(0, 0, 0, 0.2);
        background-color: white;
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        margin: auto;
        width: 350px;
        height: 350px;
        border: 2px solid rgba(0, 0, 0, 0.2);
        border-radius: 2%;
        text-align: center;
    }
    .main-window > div {
        position: absolute;
    }
    .main-window > div > button {
        display: inline-block;
        margin: 4px;
        width: 255px;
        padding: 5px 0px 5px 0px;
    }
    .main-window > div > form {
        margin-left: auto;
        margin-right: auto;
        max-width: 80%;
        text-align: center;
        font-family: "Courier New", Courier, monospace;
        color: darkslategray;
    }
    .main-window > div > form > label {
        display: absolute;
        left: 0;
        margin: 0;
    }
    .main-window > div > form > input {
        padding: 5px;
        display: inline-block;
        margin: 5px;    
    }
    .main-window > div > form > button {
        display: inline-block;
        margin: 4px;
        width: 255px;
        padding: 5px 0px 5px 0px;
    }
    .main-window > div > form > a {
        color: grey;
    }
    .match {
        color: green;
    }
    .dontmatch {
        color: red;
    }
</style>