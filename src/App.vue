<script>
export default {
    data() {
        return {
            name: "",
            card_number: "",
            expireDate: "",
            cvv: "000"
        }
    },
    methods: {
        flipCard: function () {
            var card = document.getElementsByClassName("card")

            card[0].classList.add("flip")
        },
        unflipCard: function () {
            var card = document.getElementsByClassName("card")

            card[0].classList.remove("flip")
        }
    }
}
</script> 

<template>
  <div class="bg"></div>
<div class="container">
    <div class="container-card">
        <div class="card" @mouseleave="unflipCard" @mouseover="flipCard">
            <div class="front">
                <h1>Credit Card</h1>
                <div id="card-chip">
                    <div></div>
                    <div></div>
                    <div></div>
                    <div></div>
                    <div></div>
                    <div></div>
                    <div></div>
                    <div></div>
                    <div></div>
                </div>
                <div id="card-number">{{ card_number == ""? "0000 0000 0000 0000" : card_number }}</div>
                <div id="datas">
                    <div id="card-name">{{ name == ""? "Your name here" : name}}</div>
                    <div id="card-vality">Vali:{{ expireDate != ""? expireDate : "mm/yy" }}</div>
                </div>
            </div>
            <div class="back">
                <div class="blackStrip"></div>
                <div class="whiteStrip">
                    {{ cvv == ""? "cvv" : cvv }}
                </div>
            </div>
        </div>
    </div>
    <form action="">
        <div class="row center">
            <div class="input-field s10">
                <input type="text" id="cardNumber" v-model="card_number" placeholder="ex: 1234 5678 9012 3456" required>
                <label for="cardNumber" >Número do cartão</label>
            </div>
        </div>
        
        <div class="row"></div>

        <div class="row center">
            <div class="input-field s10">
                <input type="text" id="cardName" v-model="name" placeholder="ex: Funalo Deutrano" required>
                <label for="cardName">Nome no cartão</label>
            </div>
        </div>

        <div class="row"></div>

        <div class="row space-evenly">
            <div class="input-field s3">
                <input type="text" pattern="[0-9]{2}/[0-9]{2}" v-model="expireDate" placeholder="mm/yy" required>
                <label for="expireDate">Data de expiração</label>
            </div>

            <div class="input-field s3">
                <input type="password" pattern="[0-9]{3}" id="cardCvv" v-model="cvv" placeholder="•••" required @blur="unflipCard" @focus="flipCard">
                <label for="cardCvv">CVV</label>
            </div>
        </div>

        <div class="row"></div>

        <div class="row center">
          <a href="javascript:{}" class="btn">Next</a>
      </div>
    </form>
</div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
}
body {
  background-color: #303030;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.bg {
  position: absolute;
  width: 100%;
  height: 50vh;
  background-color: blueviolet;
  left: 0;
  top: 0;
  border-radius: 0px 0px 100% 100%;
  z-index: -1;
}

.container {
  width: 400px;
  height: 350px;
  background-color: white;
  border-radius: 10px;
}

.container-card {
  position: relative;
  top: 0%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 90%;
  height: 200px;
  display: flex;
  justify-content: center;
  align-items: center;
  perspective: 800px;
}

.card {
  transition: 0.6s ease-in-out;
  transform-style: preserve-3d;
  font-family: Arial, Helvetica, sans-serif;
}

.card .front {
  position: absolute;
  width: calc(85.60px * 4);
  height: calc(53.98px * 4);
  background-image: linear-gradient(315deg, #2582ad, #033a53);
  border-radius: 18px;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  color: white;
  backface-visibility: hidden;
}

.card .front * {
  margin: 10px;
}

#card-chip {
  width: 40px;
  height: 25px;
  display: grid;
  gap: 2px;
  grid-template-rows: repeat(3, 1fr);
  grid-template-columns: repeat(3, 1fr);
}

#card-chip * {
  margin: 0;
  width: 15px;
  height: 12px;
  background-image: linear-gradient(315deg, #ecdcbb, #9c7a31);
}

#card-chip *:nth-child(1) {
  border-radius: 5px 0 0 0;
}

#card-chip *:nth-child(3) {
  border-radius: 0 5px 0 0;
}

#card-chip *:nth-child(7) {
  border-radius: 0 0 0 5px;
}

#card-chip *:nth-child(9) {
  border-radius: 0 0 5px 0;
}

#card-number {
  font-size: x-large;
  text-shadow: 2px 2px 2px rgb(0, 0, 0);
}

#datas {
  margin: 0;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  text-shadow: 2px 2px 2px rgb(0, 0, 0);
}

#card-name {
  font-size: large;
}

.card .back {
  width: calc(85.60px * 4);
  height: calc(53.98px * 4);
  background-image: linear-gradient(315deg, #2582ad, #033a53);
  border-radius: 18px;
  transform: rotateY(180deg);
  backface-visibility: hidden;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.blackStrip {
  width: 100%;
  height: 20%;
  background-color: black;
}

.whiteStrip {
  width: calc(50% - 30px);
  height: calc(15% - 30px);
  background-color: rgb(231, 231, 231);
  padding: 15px;
  margin: 15px;
  display: flex;
  justify-content: right;
  align-items: center;
  border-radius: 2px;
}

.flip {
  transform: rotateY(180deg);
}

.row {
  width: 100%;
  min-height: 20px;
  display: flex;
  align-items: center;
}

.row.center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.row.space-around {
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.row.space-evenly {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}

.input-field {
  position:relative;
}

.input-field.s3 {
  width: 24%;
}

.input-field.s6 {
  width: 49%;
}

.input-field.s10 {
  width: 82.333%;
}

.input-field input {
  width: 95%;
  height: 95%;
  border: none;
  border-bottom: 1px solid black;
  font-size: large;
  padding-top: 3px;
  padding-bottom: 1px;
}

.input-field input:focus {
  border: none;
  border-bottom: 2px solid #2582ad;
  outline: none;
}

.input-field label {
  position: absolute;
  top:0px;
left:0px;
font-size:16px;
  color: rgba(0, 0, 0, 60%);
  pointer-events:none;
  transition: 0.2s;
  white-space: nowrap;
}

.input-field input:focus ~ label,
.input-field input:valid ~ label,
.input-field input[placeholder]:not([placeholder=""]) ~ label {
  top: -12px;
  font-size:12px
}

.input-field input:focus:invalid {
  border-bottom: 2px solid crimson;
}

form {
  font-family: Arial, Helvetica, sans-serif;
  position: relative;
  left: 0;
  top: -15%;
}

.btn {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px;
  padding-left: 20px;
  padding-right: 20px;
  background-color: #2582ad;
  color: white;
  border-radius: 3px;
  text-decoration: none;
  outline: 1px rgba(0, 52, 116, .6) solid;
}
</style>
