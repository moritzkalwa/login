<template>
    <div class="main-container">
        <div class="main-window">
            <transition name="fade">
                <div id="login-window" v-if="!regstate">
                    <form class="login-form">
                        <h1>Login</h1>
                        <input type="text" id="email" name="email" v-bind:placeholder="emailplaceholder" v-model="email" pattern="/^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/" required/><br>
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
                        <input type="text" id="email" name="email" v-bind:placeholder="emailplaceholder" v-model="email" pattern="/^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/" required/><br>
                        <input type="password" id="password" name="password" placeholder="yourpassword" v-model="password" /><br>
                        <label for="conf-password">Confirm your password:</label><br>
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
                regstate: false
            }
        },
        methods: {
            log: function() {
                if(this.email != "") {
                    return false;
                } else {
                    this.emailplaceholder = "Please enter an email!";
                }
            },
            reg_trans: function() {
                this.regstate = !this.regstate;
            },
            reg: function() {

            }
        }
    }
</script>

<style>
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
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
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
</style>