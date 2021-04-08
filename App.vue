<template>
    <div>
        <div class="title">
            {{message}}
        </div>
        <div>
            <Username v-if="mode==='Username'" />
            <ChatPage :username="username" v-else-if="mode==='ChatPage'" />
        </div>
    </div>
</template>

<script>
export default {
    name: 'App',
    components: {
        Username : () => import(/* webpackChunkName: "Username" */ './components/Username'),
        ChatPage : () => import(/* webpackChunkName: "ChatPage" */ './components/ChatPage'),
    },
    data(){
        return {
            message: "Selma Chat; The New Burner Phone.",
            mode: 'Username',
            username: "",
        };
    },
    methods:{
        goToChatPage(username){
            this.username = username;
            this.mode = 'ChatPage';
        },
        goToUsernamePage(){
            this.mode = 'Username'
        }
    }
}
</script>

<style>
    .title {
        text-align: center;
        padding-top: 32px;
        margin-bottom: 32px;
        font-size: 2em;
    }
</style>