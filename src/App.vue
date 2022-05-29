<template>
<p>Arbuz</p>
<div class="form">
<form @submit.prevent="submitForm" >
<select class="farms">
  <option value="farm1">Ферма 1</option>
  <option value="farm2">Ферма 2</option>
  <option value="farm3">Ферма 3</option>
</select>
<table>
  <tr v-for="arbuz in arbuzes" :key="arbuz.id">
  <td v-for="c in arbuz" :key="c" class="pl-2" style="width: 50px">
  <img @click="addArbuz(c)" src="./assets/arbuz.png" :style="{width: '50px' , height: '50px'}">
  </td>
  </tr>                                
</table> 
<p class="visible" v-if="errors[0] == 'Error'">Выберите от 1 до 3 арбузов</p>
<p>Выбрано:</p>
<ul v-for="arbuz in formData.basket" :key="arbuz">
<li style="fontSize: 14px">{{arbuz.status}}, {{arbuz.weight}} кг</li>
</ul>
<p>Данные доставки</p>
<div class="order">
<input type="text" v-model="formData.address" placeholder="Адрес">
<p class="visible" v-if="errors[1] == 'Error'">Укажите адрес</p>
<input type="number" v-model="formData.phoneNumber" placeholder="Телефон">
<p class="visible" v-if="errors[2] == 'Error'">Укажите корректный номер телефона</p>
<input type="date" v-model="formData.date" >
<p class="visible" v-if="errors[3] == 'Error'">Укажите дату доставки</p>
<input type="time" v-model="formData.time" >
<p class="visible" v-if="errors[4] == 'Error'">Укажите время доставки</p>
<div class="checkbox">
  <input type="checkbox" v-model="formData.slice">
  <p>Порезать дольками</p>
</div>

</div>
<button type="submit" >оформить</button>
</form>
</div>
</template>

<script>
export default {
  name: 'App',
  components: {
  },
  data(){
    return{
      errors: [],
      formIsValid:false,
      formData:{
        basket: [],
        address: null,
        phoneNumber: null ,
        date: null,
        time: null,
        slice: ''
      },
      arbuzes:
      [
        [
        null,
        {
            "id": 1,
            "status": 'неспелый',
            "weight": 6300
        },
        {
            "id": 2,
            "status": 'спелый',
            "weight": 3500
        },
        {
            "id": 3,
            "status": 'спелый',
            "weight": 6300
        },
    ],
    [
        null,
        {
            "id": 5,
            "status": 'спелый',
            "weight": 6300
        },
        {
            "id": 6,
            "status": 'неспелый',
            "weight": 3500
        },
         {
            "id": 7,
            "status": 'неспелый',
            "weight": 3500
        }
    ],
    [
        null,
        {
            "id": 9,
            "status": 'спелый',
            "weight": 6300
        },
        {
            "id": 10,
            "status": 'неспелый',
            "weight": 3500
        },
         {
            "id": 11,
            "status": 'спелый',
            "weight": 3500
        }
    ],
    [
        null,
        {
            "id": 13,
            "status": 'неспелый',
            "weight": 6300
        },
        {
            "id": 14,
            "status":'спелый',
            "weight": 3500
        },
         {
            "id": 15,
            "status":'неспелый',
            "weight": 3500
        }
    ]
]
    }
  },
  methods:{
   
    addArbuz(arbuz){
      this.formData.basket.push(arbuz);
      
    },
    submitForm(){
      this.errors = [
        this.isEmpty(this.formData.basket),
        this.isFilled(this.formData.address),
        this.isNumber(this.formData.phoneNumber),
        this.isFilled(this.formData.date),
        this.isFilled(this.formData.time),
        this.isBoolean(this.formData.slice)
      ]
      if(
      this.formData.address != null &&
      this.formData.phoneNumber != null &&
      this.formData.date != null &&
      this.formData.time != null
      ){
        this.formIsValid = true;
      }
      if(this.formIsValid){
        this.formData.basket = [],
        this.formData.address=null,
        this.formData.phoneNumber=null,
        this.formData.date=null,
        this.formData.time=null,
        this.formData.slice=null
      }
      else{
        console.log('Invalid form')
      }
    },
    isFilled(value){
      return  !value ? "Error" : null;
    },
    isNumber(value){
      if(!value || value.toString().length != 11){
        return 'Error';
      }
      else{
        return null
      }
    },
    isBoolean(value) {
      if (typeof value === "boolean") {
        return null;
      } else {
        return "Error";
      }
    },
    isEmpty(value){
      if(value.length === 0  || value.length >3){
        return 'Error'
      }
      else{
        return null
      }
    }

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
}
.form{
  width: 100%;
  height: auto;
  display: flex;
  justify-content: center;
}
form{
  width: 40%;
  height: auto;
  border: 2px solid black;
  display: flex;
  flex-direction: column;
  align-items:center;
  justify-content: center;
}
.farms{
  width: 30%;
  height: 30px;
  margin-top: 5px;
}
table{
  margin: 0 auto;
  margin-top: 10px
}
.order{
  display: flex;
  flex-direction: column;
  width: 100%;
  align-items: center;
}
input{
  width: 40%;
  height: 40px;
  margin: 5px;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  outline: none;
  -webkit-transition: 0.5s;
  transition: 0.5s;
}
input:focus{
  border: 1px solid #4CAF50;
}
.checkbox{
  width: 40%;
  display: flex;
  align-items: center;
  
}
.checkbox input{
  width: 10%;
  height: 20px;
  margin-right: 10px
}
.visible{
  color: red;
  font-size: 14px;
  margin-top: 2px;
}
button{
  width: 15%;
  background-color: #4CAF50;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
button:hover{
  background-color: #45a049;
}
@media only screen and (max-width : 420px) {
  form{
    width: 70%;
  }
  input{
    width: 80%;
  }
  button{
    width: 40%;
    height: 30px;
    display: flex;
    align-items: center;
  }
}
@media only screen and (max-width : 768px) {
  form{
    width: 80%;
  }
  input{
    width: 80%;
  }
  button{
    width: 30%;
    height: 30px;
    display: flex;
    align-items: center;
  }
}
</style>
