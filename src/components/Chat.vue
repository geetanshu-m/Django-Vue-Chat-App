<template>
  <div id="chat-container">
      <div id="messages">
          <Messages
                v-for="(chat,index) in chats"
                :key="index"
                :message="chat"
                :deleteMsg="deleteMsg"
            />
      </div>
    <div id="text-box">
        <textarea v-model="body"/>
        <button @click="sendMessage">Submit</button>
    </div>
  </div>
</template>

<script>
import Messages from './messages'
import messageService from '../services/messageService'
export default {
    name:"chat-container",
    components:{
        Messages
    },
    data(){
        return{
            body:"",
            chats:[]
        }
    },
    methods:{
        sendMessage(){
            let payload = {
                body:this.body,
                subject:"u3"
            }
            messageService.postMessage(payload).then(response => {
                console.log(response.data)
                this.chats.push(payload)
            })
            
            // messageService.fetchMessages().then(response => {
            //     console.log(response)
            // })
        },
        deleteMsg(pk){
            messageService.deleteMessage(pk)
            this.chats = this.chats.filter(obj => obj.pk !== pk)
        }
    },
    async mounted(){
        this.chats =await messageService.fetchMessages()
    }

}
</script>

<style scoped>
#chat-container{
    display:flex;
    flex-direction: column;
    height: 100vh;
}
#messages{
    flex-direction: column;
    flex:1;
    display:flex;
    overflow-y:auto;
}
#text-box{
    height:100px;
}
</style>