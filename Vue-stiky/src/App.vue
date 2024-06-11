<script setup>
import { ref } from 'vue';


  const showform = ref(false);
  const newMemo = ref("");
  const memos = ref([]);
  const errormassage = ref("");


  function addMemo (){
    if(!newMemo.value){
      errormassage.value ="Please enter a teks in bellow! "
      return;
    }
    memos.value.push({
      id: Date.now,
      memo: newMemo.value,
      date: new Date().toLocaleDateString("en-us"),
      backgroundcolor: getrandomcolor(),
    });
    newMemo.value ="";
    showform.value= false;

  }

  function getrandomcolor(){
   return  `#${Math.floor(Math.random()*16777215).toString(16)}`;
  }

  function deleteMemo(id){
    memos.value = memos.value.filter((memo) => memo.id !== id);
  }


</script>


<template>
 <main>
  {{ memos }}
  <div class="container">
    <header>
      <h1 class="header-title">Memo</h1>
      <button  @click="showform = true"  class="header-button">+</button>
    </header>
    <div class="card-container">
      <div v-for="(memo,index) in memos" :key="index"  class="card"   :style="{ backgroundColor: memo.backgroundcolor }">
        <p class="card-content">{{memo.memo }}</p>
        
        <div class="card-footer">
          <p class="card-date">{{ memo.date }}</p>
          <button @click="deleteMemo(memo.id)" class="card-button">x</button>
        </div>

      </div>
    </div>
  </div>

  <div  v-if="showform"  class="form-overlay">

    <div class="form-modal">
      <button @click="showform = false"   class="form-close-btn">&times;</button>
      <p v-if="errormassage" class="form-error" >{{ errormassage }}</p>
      <textarea v-model="newMemo"    name="memo" id="memo" cols="30" rows="10"></textarea>
      <button @click="addMemo" class="form-save-btn">Save</button>
    </div>

  </div>

 </main>
</template>


<style scoped>
  main{
    height: 100vh;
    width: 100vw;
  }

  .container{
    max-width: 900px;
    padding: 10px;
    margin: 0 auto;
  }

  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .header-title{
    font-size: 48px;
    font-weight: bold;
    margin-bottom: 25px;
    color: gray;
  }

  .header-button{
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    border-radius: 100%;
    background-color: black;
    color: white;
  }


  .card{
    width: 255px;
    height: 255px;
    padding: 10px;
    background-color: aqua;
    margin-bottom: 25px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    border-radius: 25px;
    cursor: pointer;
  }

  .card-footer{
    display: flex;
    justify-content: space-between;
    align-items: center;

  }
 
  
  .card-container{
    display: flex;
    flex-wrap: wrap;
    gap: 20px ;
  }


  .form-overlay{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgb(0,0,0,0.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .form-modal{
    width: 420px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  .form-save-btn{
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: black;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    margin-top: 15px;
    color: white;
  }

  .form-close-btn{
    position: absolute;
    top: 5px;
    right: 10px;
    width: 30px;
    height: 30px;
    background-color:transparent;
    border: none;
    font-size: 30px;
    cursor: pointer;

  }

  .form-error{
    color: red;

  }




</style>