<template>
    <form class="mt-5" @submit.prevent ="enterUser">
        <div class="form-group">
            <label for="email">Ваш email:</label>
            <input type="email" class="form-control" id="email" placeholder="Введите email:" required v-model="user.email">
        </div>
        <div class="form-group">
            <label for="password">Ваш пароль:</label>
            <input type="password" class="form-control" id="password" placeholder="Введите пароль:" required v-model="user.password">
        </div>
        <div class="alert alert-danger" role="alert" v-if="error2">
            <strong>Ой!</strong>Неверно указана почта или пароль.
        </div>
        <button type="submit" class="btn btn-primary">Войти</button>
        
    </form>
</template>
<script>
    export default {
        data(){
            return{
            user: {
                email:  '',
                password: ''
                },
            error2: false
            }
        },
        methods: {
            enterUser(){
                firebase.auth().signInWithEmailAndPassword(this.user.email, this.user.password)
                    .then(response => {
                        console.log(response)
                        const sett = {
                            email: response.user.email,
                            uid: response.user.uid,
                            mainPage: true,
                            complete: true
                        }
                        this.$emit('addUser', sett);
                    })
                    .catch(response => {
                        if(Error){
                            this.error2 = true;
                        }
                    })
                    
                    
            }
        }
        
    }
    
</script>