<template>
    <form class="mt-5" @submit.prevent="registerUser">
        <div class="form-group">
            <label for="email">Ваш email:</label>
            <input type="email" class="form-control" id="email" placeholder="Введите email:" required v-model="user.email">
        </div>
        <div class="form-group">
            <label for="password">Ваш пароль:</label>
            <input type="password" class="form-control" id="password" placeholder="Введите пароль (от 6 символов):" required v-model="user.password">
        </div>
        <div class="form-group">
            <label for="password2">Повтрите пароль:</label>
            <input type="password" class="form-control" id="password2" placeholder="Повтрите пароль:" required v-model="user.confirmPassword">
        </div>
        <div class="alert alert-danger" role="alert" v-show="error">
            <strong>Ой!</strong>Пароли не совпадают или вы забыли их ввести.
        </div>
        <button type="submit" class="btn btn-primary">Зарегистрироваться</button>
    </form>
</template>
<script>
    export default {
        name: 'sign-up',
        data(){
            return {
                user: {
                    email: '',
                    password: '',
                    confirmPassword: ''
                },
                error: false
            }
        },
        methods: {
            registerUser(){
            if(this.user.password !== this.user.confirmPassword || this.user.password.length<6){
                this.error = true;
                } else{
                    firebase.auth().createUserWithEmailAndPassword(this.user.email, this.user.password)
                        .then( () => {
                            this.$emit('regSuccess', 'sign-in')
                        })
                        .catch( error => {
                            console.log(error)
                        })
                }
            }
        }
    }

</script>