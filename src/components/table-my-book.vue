<template>
    <div>
    <h1>books that I have to read</h1>
    <form>
        <div class="wrapper">
            <div class="new-book">
                <input type="text" 
                placeholder="NEW-BOOK"
                v-model="names">
            </div>
            <div class="priority" >
                <input type="number"
                 placeholder="0"
                 v-model="priority">
            </div>
        </div>
     <button @click.prevent="send">ADD</button>
    </form>
    <div class="wrapper-head">
    <div>Name-book</div>
    <div>Priority</div>
    <div>read</div>
    <div>not-read</div>
    </div>
    <div class="wrapper-content" v-for="(list, index ) in listBook" :key="index" >
        <div class="name-book">{{list.item}}</div>
        <div class="priority">{{ list.priority }}</div>
        <div class="read">
        <input type="checkbox"></div>
        <div class="not-read">
        <input type="checkbox"></div>
        <div class="deleteBook"><button @click.stop="removeBook(index)">X</button></div>
    </div>

    </div>
</template>
<script>
export default {
    name:'My_book',
data(){
    return{
            names:"",
            priority: 0, 
        listBook: [],
    }
    },
    mounted(){
        if(localStorage.getItem('listBook'))
          this.listBook = JSON.parse(localStorage.getItem('listBook'));
    },
methods: {
        send(){
            if(this.names !== '' && this.priority !== 0  ){
                this.listBook.push({
   item: this.names,
   priority: this.priority,
} );
this.saveList();
this.names = '';
this.priority = 0;
            }

        },
         removeBook(x){
this.listBook.splice(x,1);
console.log(x);
this.saveList();
        },
        saveList(){
            let parsed = JSON.stringify(this.listBook);
            localStorage.setItem('listBook', parsed)
        }
       
}
  
}
</script>
<style>
h1{
    font-size: 35px;
    text-align: center;
    margin-top: 30px;
    color: rgb(63, 59, 59);
    text-transform: uppercase;
}
.wrapper{
    width: 460px;
    display: grid;
    grid-template-columns: 400px 60px;
    margin: 0 auto;
}
input{
    height: 40px;
    font-size: 24px;
}
.priority input{
    width: 40px;
}
button{
    display: block;
   margin: 20px auto;
    width: 100px;
    height: 40px;
    color: #fff;
    background-color: #000;
    font-size: 35px;
    cursor: pointer;
}
.wrapper-content{
    display: grid;
    grid-template-columns: 400px 60px 40px 40px 40px;
    margin: 0 auto;
    width: 580px;
    height: 40px;
    font-size: 14px;
}
.deleteBook button{
    width: 40px;
    height: 40px;
   text-align: center;
   padding-top: 10px;
   font-size: 24px;
   margin: 0;
}
.deleteBook button:hover{
    color: rgb(255, 36, 36);
}
.wrapper-content .name-book,
.wrapper-content .priority{
    display: flex;
    justify-content: center;
    align-items: center;
}
.wrapper-content input{
    width: 30px;
    height: 30px;
}
.wrapper-content div{
    border: 2px solid #000;
}
.wrapper-head{
    display: grid;
    grid-template-columns: 400px 60px 30px 60px;
    width: 540px;
    margin: 10px auto;
}
.wrapper-head div{
    display: flex;
    justify-content: center;
}
</style>