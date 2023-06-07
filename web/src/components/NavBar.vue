<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container">
            <router-link :to="{name: 'home'}" class="navbar-brand">King Of Bots</router-link>
            <div id="navbarText" class="collapse navbar-collapse">
                <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                    <li class="nav-item">
                        <router-link :class="route_name === 'pk_index' ? 'nav-link active' : 'nav-link'"
                                     :to="{name: 'pk_index'}">对战
                        </router-link>
                    </li>
                    <li class="nav-item">
                        <router-link :class="route_name === 'record_index' ? 'nav-link active' : 'nav-link'"
                                     :to="{name: 'record_index'}">对局列表
                        </router-link>
                    </li>
                    <li class="nav-item">
                        <router-link :class="route_name === 'ranklist_index' ? 'nav-link active' : 'nav-link'"
                                     :to="{name: 'ranklist_index'}">排行榜
                        </router-link>
                    </li>
                </ul>
                <ul v-if="$store.state.user.is_login" class="navbar-nav">
                    <li class="nav-item dropdown">
                        <a id="navbarDropdown" aria-expanded="false" class="nav-link dropdown-toggle" data-bs-toggle="dropdown"
                           href="#" role="button">
                            {{ $store.state.user.username }}
                        </a>
                        <ul aria-labelledby="navbarDropdown" class="dropdown-menu">
                            <li>

                                <router-link :to="{name: 'user_bot_index'}" class="dropdown-item">我的Bot</router-link>
                            </li>
                            <li>
                                <hr class="dropdown-divider">
                            </li>
                            <li><a class="dropdown-item" href="#" @click="logout">退出</a></li>
                        </ul>
                    </li>
                </ul>
                <ul v-else-if="!$store.state.user.pulling_info" class="navbar-nav">
                    <li class="nav-item">
                        <router-link :to="{name: 'user_account_login' }" class="nav-link" role="button">
                            登录
                        </router-link>
                    </li>
                    <li class="nav-item">
                        <router-link :to="{name: 'user_account_register'}" class="nav-link" role="button">
                            注册
                        </router-link>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>

<script>
import {useRoute} from 'vue-router'
import {computed} from 'vue'
import {useStore} from 'vuex';

export default {
    setup() {
        const store = useStore();
        const route = useRoute();
        let route_name = computed(() => route.name)

        const logout = () => {
            store.dispatch("logout");
        }

        return {
            route_name,
            logout
        }
    }
}
</script>

<style scoped>

</style>