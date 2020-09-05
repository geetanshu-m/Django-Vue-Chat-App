<template>
  <div id="chat-message">
      <div>
        {{message.subject}} => {{message.body}}
        </div>
        <div @click="deleteMsg(message.pk)">
            X
        </div>
  </div>
</template>

<script>
export default {
    name:"chat-message",
    props:[
        'message',
        'deleteMsg'
    ]
}
</script>

<style scoped>
#chat-message{
    display:flex;
    flex-direction: row;
    justify-content: space-between;
    margin: 0px 100px;
}
</style>