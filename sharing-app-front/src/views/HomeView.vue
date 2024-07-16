<script setup>
import axios from 'axios'
import { ref } from 'vue'
const text = ref('')
const link = ref('')

const sendText =  async ()=>{
  if (text.value.trim()) {
    try{
      const response =await axios.post('http://localhost:5050/texts',{
        content: text.value
      });
      link.value = `${window.location.origin}/text/${response.data.id}`
      text.value =''
    }catch{
      console.log("you have a Error :",error);
    }
  }
}
</script>


<template>
    <div class="text-input">
        <h2>Write and Share Text</h2>
        <form class="text-form" @submit.prevent="sendText()">
            <textarea  placeholder="Write your text here..." v-model="text" class="textarea">
          </textarea>
          <button class="myButton" type="submit">Save and get Link</button>
        </form>
        <p v-if="link">Share this link: <a :href="link">{{ link }}</a></p>
    </div>
</template>


<style scoped>
.text-input {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    height: 50dvh;
}
.text-form{
  margin: 1rem;
  width: 70%;
}
.text-form > textarea{
  box-shadow: rgba(240, 46, 170, 0.4) -5px 5px, rgba(240, 46, 170, 0.3) -10px 10px, rgba(240, 46, 170, 0.2) -15px 15px, rgba(240, 46, 170, 0.1) -20px 20px, rgba(240, 46, 170, 0.05) -25px 25px;
  border-radius: 4px;
  width: 100%;
  padding: .5rem;
  height: 10rem;
  font-size: larger;

}

.myButton {
  margin: 20px 20px;
  width: 90%;
	box-shadow:inset 0px 1px 0px 0px #e184f3;
	background:linear-gradient(to bottom, #c123de 5%, #a20dbd 100%);
	background-color:#c123de;
	border-radius:6px;
	border:1px solid #a511c0;
	display:inline-block;
	cursor:pointer;
	color:#ffffff;
	font-family:Courier New;
	font-size:medium;
	font-weight:bold;
	padding:6px 20px;
	text-decoration:none;
	text-shadow:0px 1px 0px #9b14b3;
}
.myButton:hover {
	background:linear-gradient(to bottom, #a20dbd 5%, #c123de 100%);
	background-color:#a20dbd;
}
.myButton:active {
	position:relative;
	top:1px;
}

</style>