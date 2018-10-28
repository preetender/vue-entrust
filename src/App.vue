<template>
    <div id="app">

        <h1>Qualquer coisa!</h1>

        <role name="user">Tem usuário</role>

        <role name="admin">Tem admin</role>

        <role name="user|admin" strict>
            Tem user e admin
        </role>

        <role name="user|admin">
            Tem user ou admin
        </role>

        <role name="moderator">
            Tem user ou admin
            <div slot="error">Opa! Você não tem permissões de moderador.</div>
        </role>

        <role name="user|admin|dev" strict>
            Tem user,admin e dev

            <div slot="error">Opa! todos os papeis são requeridos.</div>
        </role>
    </div>
</template>

<script>
    import {Role} from './index'

    export default {
        name: 'App',

        components: {
            Role
        }
    }
</script>
