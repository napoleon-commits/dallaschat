<template>
    <div>
        <div style="text-align: center; font-size: 1.5em;">Your Username: {{username}}</div>
        <div id="chat-box">
            <br />
            <br />
            <div v-for="(obj, i) in chat" :key="i">
                <div :style="`${(obj.username === username)?'text-align: right;':''}`">
                    <div
                        :style="`${
                            (obj.username === username)
                            ? 'font-weight: bold; margin-right: 2%;'
                            : 'font-weight: bold; margin-left: 2%;'
                        }`"
                    >
                        {{obj.username}}
                    </div>
                    <div
                        :style="`${
                            (obj.username === username)
                            ?'margin-left: 48%; margin-right: 2%;'
                            :'width: 48%; margin-left: 2%;'}`"
                    >
                        {{obj.message}}
                    </div>
                </div>
                <br />
                <br />
            </div>
            <br />
            <br />
        </div>
        <div id="toolbar">
            <input
                v-model="receiver"
                style="width: 99%;"
                type="text"
                :placeholder="`Receiver's Username`"
                v-on:keyup.enter="sendMessage"
            /><br />
            <input
                v-model="message"
                style="width: 99%;"
                type="text"
                placeholder="Type message here:"
                v-on:keyup.enter="sendMessage"
            /><br/>
            <button @click="sendMessage">Send</button>
        </div>
    </div>
</template>

<script>
import PrivateVariables from '../PrivateVariables';

export default {
    name: 'ChatPage',
    props: ['username'],
    data(){
        return {
            chat: [],
            connection: null,
            PrivateVariables,
            receiver: '',
            message: '',
        };
    },
    created(){
        this.connection = new WebSocket(`${PrivateVariables.wssURL}${this.username}`);
        this.connection.onmessage = (event) => {
            const dataObject = JSON.parse(event.data);
            this.chat.push({
                username: dataObject.sender,
                message: dataObject.message,
            });
        };
        this.connection.onclose = () => {
            this.$parent.goToUsernamePage();
        }
    },
    methods: {
        sendMessage: function() {
            if(this.message.length > 0 && this.receiver.length > 0){
                const messageObject = {
                    sender: this.username,
                    receiver: this.receiver,
                    message: this.message,
                    action: "message",
                };
                this.connection.send(JSON.stringify(messageObject));
                this.chat.push({
                    username: `${this.username}`,
                    message: this.message,
                });
                this.message = '';
            }
        }
    },
}
</script>

<style>
    #chat-box{
        height: 50vh;
        width: 85.41019662496846%;
        border: 2px solid black;
        border-radius: 8px;
        margin: auto;
        overflow: scroll;
    }
    #toolbar{
        width: 85.41019662496846%;
        margin: auto;
    }
</style>