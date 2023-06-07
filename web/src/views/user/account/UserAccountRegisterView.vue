<template>
    <ContentField>
        <div class="row justify-content-md-center">
            <div class="col-3">
                <form @submit.prevent="register">
                    <div class="mb-3">
                        <label class="form-label" for="username">用户名</label>
                        <input id="username" v-model="username" class="form-control" placeholder="请输入用户名"
                               type="text">
                    </div>
                    <div class="mb-3">
                        <label class="form-label" for="password">密码</label>
                        <input id="password" v-model="password" class="form-control" placeholder="请输入密码"
                               type="password">
                    </div>
                    <div class="mb-3">
                        <label class="form-label" for="confirmedPassword">确认密码</label>
                        <input id="confirmedPassword" v-model="confirmedPassword" class="form-control" placeholder="请再次输入密码"
                               type="password">
                    </div>
                    <div class="error-message">{{ error_message }}</div>
                    <button class="btn btn-primary" type="submit">提交</button>
                </form>
            </div>
        </div>
    </ContentField>
</template>

<script>
import ContentField from '../../../components/ContentField.vue'
import {ref} from 'vue'
import router from '../../../router/index'
import $ from 'jquery'

export default {
    components: {
        ContentField
    },
    setup() {
        let username = ref('');
        let password = ref('');
        let confirmedPassword = ref('');
        let error_message = ref('');

        const register = () => {
            $.ajax({
                url: "http://127.0.0.1:3000/user/account/register/",
                type: "post",
                data: {
                    username: username.value,
                    password: password.value,
                    confirmedPassword: confirmedPassword.value,
                },
                success(resp) {
                    if (resp.error_message === "success") {
                        router.push({name: "user_account_login"});
                    } else {
                        error_message.value = resp.error_message;
                    }
                },
            });
        }

        return {
            username,
            password,
            confirmedPassword,
            error_message,
            register,
        }
    }
}
</script>

<style scoped>
button {
    width: 100%;
}

div.error-message {
    color: red;
}
</style>