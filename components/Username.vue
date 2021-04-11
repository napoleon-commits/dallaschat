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
        <div id="warning-container">
            Choose a unique name. Someone with the same username
            will override your existing connection.
        </div><br>
        <div id="warning-container">
            Usernames are no longer kept when the connection is lost.
        </div><br>
        <div id="warning-container">
            No messages are saved.
        </div><br>
        <div id="warning-container">
            Usernames are case-sensitive.
        </div><br>
        <div id="warning-container">
            A connection will be lost if the user refreshes the app, if the user exits the app, or if the connection is idle for an hour.
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
                alert(`Username can't be empty.`);
            } 
            else if(new RegExp('^[a-zA-Z0-9_.-]*$').test(this.username) === false){
                alert(`Username can only be letters and numbers and have no spaces.`);
            }
            else {
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
    #warning-container{
        width: 85.41019662496846%;
        margin: auto;
    }
</style>