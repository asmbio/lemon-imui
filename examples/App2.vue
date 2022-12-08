<template>
  
    <lemon-imui id="app"
    width="100%"
    height="100%"   
    
      :user="user"
      ref="IMUI"
      hideMenu=true
      @pull-messages="handlePullMessages"
      @message-click="handleMessageClick"
      @send="handleSend"
      
    >
      <template #cover>
        <div class="cover">
          <span><b>Maons</b> IMUI</span>
        </div>
      </template>
    </lemon-imui>
  <!-- //  <button @click="layout" >修改高度</button> -->
  
</template>

<script>
const getTime = () => new Date().getTime();
const generateRandId = () => Math.random().toString(36).substr(-8);
//   changeMenu = function(num) {
//   this.$refs.IMUI.changeMenu(num);
// }

// const toPx = val => {
//   return isString(val) ? val : `${val}px`;
// };

export default {
  name: "App",
  components: {},
  data() {
    return {
      user: {
        id: "1",
        displayName: "June",
        avatar: "",
      },
    };
  },
  mounted() {
    const { IMUI } = this.$refs;
    window.factorial=  function factorial (num) {
        if (num === 0 || num === 1)
            return 1;
        for (var i = num - 1; i >= 1; i--) {
            num *= i;
        }
        return num;
    };
    window.IMUI=  IMUI;
    // window.changeMenu= function    (num){
      
    //   IMUI.changeMenu(num);
    //   return 1;
    // };
    
    
    
    IMUI.initContacts([
      {
        id: "2",
        displayName: "铁柱子",
        avatar: "",
        type: "single",
        index: "T",
        unread: 0,
        lastSendTime: getTime(),
        lastContent: "你好123",
      },
      {
        id: "3",
        displayName: "铁柱子",
        avatar: "",
        type: "single",
        index: "T",
        unread: 0,
        lastSendTime: getTime(),
        lastContent: "你好123",
      },
      {
        id: "4gggggg",
        displayName: "铁柱子",
        avatar: "",
        type: "single",
        index: "T",
        unread: 0,
        lastSendTime: getTime(),
        lastContent: "你好123",
      },
      {
        id: "5",
        displayName: "铁柱子",
        avatar: "",
        type: "single",
        index: "T",
        unread: 0,
        lastSendTime: getTime(),
        lastContent: "你好123",
      },
      {
        id: "6",
        displayName: "铁柱子",
        avatar: "",
        type: "single",
        index: "T",
        unread: 0,
        lastSendTime: getTime(),
        lastContent: "你好123",
      },
    ]);
  
     // IMUI.changeContact("2");

  },
  methods: { 
    layout(w,h) {
      console.log(w,h);
      const { IMUI } = this.$refs;
      IMUI.width= w;
      IMUI.height =h;
    },
    // changeMenu  (num){
    //   const { IMUI } = this.$refs;
    //   IMUI.changeMenu(num);
    //   return 1;
    // },
    handleMessageClick(e, key, message) {
      const { IMUI } = this.$refs;
      if (key == "status" && message.status === "failed") {
        IMUI.updateMessage({
          id:message.id,
          toContactId:message.toContactId,
          status: "going",
          content: "重新发送消息...",
        });
        setTimeout(() => {
          IMUI.updateMessage({
            id:message.id,
            toContactId:message.toContactId,
            status: "failed",
            content: "还是发送失败",
          });
        }, 2000);
      }
    },
    handleSend(message, next, file) {
      console.log(message, next, file);
      setTimeout(() => {
        next({
          status: "failed",
        });
      }, 1000);
    },
    handlePullMessages(contact, next) {
      const { currentContactId } = this.$refs.IMUI;
      const otherUser = {
        id: contact.id,
        avatar: contact.avatar,
        displayName: contact.displayName,
      };
      const message = (content, fromUser = this.user) => {
        return {
          id: generateRandId(),
          status: "succeed",
          type: "text",
          sendTime: getTime(),
          content,
          toContactId: currentContactId,
          fromUser,
        };
      };

      const messages = [
        message("再bb，信不信我盗你号？", otherUser),
        message("来"),
        message("别后悔", otherUser),
      ];
      next(messages, true);
    },
  },
};
</script>

<style>
html{
  height: 100%;
  margin: 0px;
}
body {
  height: 100%;
  margin: 0px;
  /* background: rgb(251, 249, 249); */
  /* display: flex;
  justify-content: center;
  padding-top: 0px; */
}
.cover {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 24px;
  color: #ddd;
}

</style>