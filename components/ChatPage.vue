<template>
    <div>
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
            <input style="width: 48%;" type="text" :placeholder="`Receiver's Username`"/><br />
            <input style="width: 48%;" type="text" placeholder="Type message here:"/><br/>
            <button>Send</button>
        </div>
    </div>
</template>

<script>
import MockChat from '../mocks/MockChat';

export default {
    name: 'ChatPage',
    props: ['username'],
    data(){
        return {
            chat: MockChat,
        };
    }
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