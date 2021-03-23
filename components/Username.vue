<template>
    <div id="username-container">
        <br />
        <input
            style="text-align: center;"
            type="text"
            v-model="username"
            placeholder="Choose a username."
            v-on:keyup.enter="goToChatPage"
        />
        <br /><br />
        <button @click="goToChatPage">Submit</button><br /><br />
        <div>**WARNING**</div><br />
        <div>
            Choose a unique name. Someone with the same username can
            see your messages and send messages as you.
        </div><br>
    </div>
</template>

<script>
export default {
    name: 'Username',
    data(){
        return {
            username: '',
        }
    },
    methods: {
        goToChatPage(){
            if(this.username === ''){
                alert(`Username can't be empty`);
            } else {
                this.$parent.goToChatPage(this.username);
            }
        }
    }
}
</script>

<style>
    #username-container{
        border: 2px solid black;
        border-radius: 8px;
        width: 85.41019662496846%;
        margin: auto;
        text-align: center;
    }
</style>