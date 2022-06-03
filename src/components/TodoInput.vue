<template>
    <div class="inputBox sahdow">
        <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
        <!-- <button @click="addTodo">add</button> -->
        <span class="addContainer" @click="addTodo">
            <i class="fas fa-plus addBtn" aria-hidden="true"></i>
        </span>
    </div>
</template>

<script>
export default {
  data: function() {
    return {
      newTodoItem: ""
    }
  },
  methods: {
        addTodo(){
            //inputbox 빈값인지 체크, 빈값이 아니면 로직 수행
            if(this.newTodoItem !== ''){
                //inputbox에 입력된 텍스트의 앞, 뒤 공백문자열 제거
                var value = this.newTodoItem && this.newTodoItem.trim();
                //App컴포넌트로 이벤트 전달
                this.$emit('addTodo', value);
                //inputbox 초기화
                this.clearInputbox();
            }
        },
        clearInputbox(){
            this.newTodoItem = '';
        }
    }
}
</script>

<style scoped>
input:focus{
    outline:none;
}
.inputBox{
    background:white;
    height:50px;
    line-height:50px;
    border-radius:5px;
}
.inputBox input{
    border-style:none;
    font-size:0.9rem;
}
.addContainer{
    float:right;
    background:linear-gradient(to right, #62EAC6, #32CEE6);
    display:block;
    width:3rem;
    border-radius:0 5px 5px 0;
}
.addBtn{
    color:white;
    vertical-align:middle;
}
</style>