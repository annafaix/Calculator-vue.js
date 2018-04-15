<template>
  <div id="calcWrap">
	<h1>Calculator Vue.js</h1>
  <input v-model="current" type="number" placeholder="0" autofocus/>
	<div>Saved number: {{ current }}</div>
  <div>Result: {{ result }} </div>

	<div class="buttonWrap">
		<div class="left">
			<div v-bind:class="digitBtn">
				<button v-on:click="doMath">7</button>
				<button v-on:click="doMath">8</button>
				<button v-on:click="doMath">9</button>
			</div>
			<div v-bind:class="digitBtn">
				<button v-on:click="doMath">4</button>
				<button v-on:click="doMath">5</button>
				<button v-on:click="doMath">6</button>
			</div>
			<div v-bind:class="digitBtn">
				<button v-on:click="doMath">1</button>
				<button v-on:click="doMath">2</button>
				<button v-on:click="doMath">3</button>
			</div>
			<div v-bind:class="digitBtn">
				<button v-on:click="doMath">0</button>
			</div>
		</div>

		<div class="right">
			 <div v-bind:class="operatorBtn">
				<button v-on:click="doMath" >+</button>
				<button v-on:click="doMath" >-</button>
			</div>
			<div v-bind:class="operatorBtn">
				<button v-on:click="doMath">*</button>
				<button v-on:click="doMath">/</button>
			</div>
			<div v-bind:class="operatorBtn">
				<button v-on:click="doMath">x2</button>
				<button v-on:click="doMath" v-if="negativeNum">√</button>
			</div>
			<div>
				<button v-bind:class="clearBtn" v-on:click="clear">C</button>
				<button v-on:click="getResult" v-bind:class="equal">=</button>
			</div>
		</div>
</div>
  <div>History {{ history }}</div>
</div>
</template>

<!-- TODO
- inputfälte registreras inte ibland !important
- mellanresultat visas inte
- funktion för operationerna x2 och √ (roten ur)
- räkna rätt! en mellanresultat

-->

<script>
    export default{

    name: 'calcWrap',
    data: function(){
      return{
				current: '',
				saved:0,
        result: 0,
        history: [],
        equal: 'equal',
				clearBtn: 'clearBtn',
        operatorBtn: 'operatorBtn',
				digitBtn: 'digitBtn',
        negativeNum: true,
      };
    }, //data
    methods:{
			doMath: function(event){
        let value = event.target.innerText;
        if(value !== "+" && value !== "-" && value !== "*" && value !== "/" && value !== "="){
          this.current += value;
          console.log(value);
        }else{
          switch(value){
            case "+":
              this.current += event.target.innerText;
              break;

            case "-":
              this.current += event.target.innerText;
              break;

            case "*":
              this.current += event.target.innerText;
              break;

            case "/":
              this.current += event.target.innerText;
              break;
          }
        }

			},
      getResult: function(event){
        this.result = eval(this.current);
        if(this.result < 0){
          this.negativeNum = false;
          console.log(this.negativeNum);
        }else{
          this.negativeNum = true;
        };
        console.log(this.result);
        if (this.result !== undefined) {
          this.history.unshift(this.result)
          if(this.history.length >= 5){
            this.history.pop();
          }
          this.current = this.result;
        }
      },


			clear:function(event){
				this.current = '';
				this.result = '';
				console.log(this.current);
			}
    }// methods
  }; //Vue object

</script>

<!-- CSS libraries -->
<style src="normalize.css/normalize.css"></style>

<!-- Global CSS -->
<style>
body {
  align-items: center;
  box-sizing: border-box;
  /*  background-color: #020205; */
  color: #FFFFFF;
  display: flex;
  /* font-size:25px; */
  flex-direction: row;
  justify-content: center;
  margin: 20px;
}

</style>

<!-- Scoped component css -->
<!-- It only affect current component -->
<style scoped>
  #calcWrap{
    background-color: #111F4D;
    box-shadow: 10px 10px 35px 0px rgba(0,0,0,0.75);
    color:#FFFFFF;
    display: flex;
    flex-direction: column;
    font-family: 'Roboto Mono', monospace;
    margin:0;
    padding: 15px;
    text-align: center;
    width: 350px;
  }
  .buttonWrap{
    display:flex;
    justify-content: space-between;
    flex-flow: row wrap;
  }
  #calcWrap>input{
    height: 40px;
    font-weight: bold;
    text-align: right;
    font-family:courier;
    font-size: 30px;
  }
  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
   /* display: none; <- Crashes Chrome on hover */
   -webkit-appearance: none;
   margin: 0; /* <-- Apparently some margin are still there even though it’s hidden */
  }
  .digitBtn>*{
    background-color: #E43A19;
    border: none;
    border-radius:5px;
    box-shadow: 10px 10px 35px 0px rgba(0,0,0,0.75);
    color: #FFFFFF;
    font-size: 25px;
    font-weight: bold;
    margin:3px;
    width: 50px;
    height: 50px;
  }
  .operatorBtn>*{
    background-color: #C00000;
    border: none;
    border-radius:5px;
    box-shadow: 10px 10px 35px 0px rgba(0,0,0,0.75);
    color: #FFFFFF;
    font-size: 25px;
    font-weight: bold;
    margin:3px;
    width: 50px;
    height: 50px;
  }
  .equal{
    background-color: #FFFFFF;
    color: #C00000;
    border: none;
    border-radius:3px;
    box-shadow: 10px 10px 35px 0px rgba(0,0,0,0.75);
    font-size: 25px;
    font-weight: bold;
    margin:3px;
    height:40px;
    width: 50px;
  }
  .clearBtn{
    background-color: #FFFFFF;
    border: none;
    border-radius:5px;
    box-shadow: 10px 10px 35px 0px rgba(0,0,0,0.75);
    color:#C00000;
    font-size: 25px;
    font-weight: bold;
    margin:3px;
    height:40px;
    width:50px;
  }
  .operatorBtn>button:hover, .digitBtn>button:hover, .equal:hover{
    color: #111F4D;
  }

</style>
