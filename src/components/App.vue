<template>
  <div id="calcWrap">
	<h1>Calculator Vue.js</h1>
  <input v-model="current"  type="number" v-bind:placeholder="placeholder" autofocus/>
  <div>Current number: {{ current }}</div>
	<div>Saved number: {{ saved}}</div>
  <div>Result: {{ result }} </div>

	<div class="buttonWrap">
		<div class="left">
			<div class="digitBtn">
				<button value="7" v-on:click="getNumber('7')">7</button>
				<button value="8" v-on:click="getNumber('8')">8</button>
				<button value="9" v-on:click="getNumber('9')">9</button>
			</div>
			<div class="digitBtn">
				<button value="4" v-on:click="getNumber('4')">4</button>
				<button value="5" v-on:click="getNumber('5')">5</button>
				<button value="6" v-on:click="getNumber('6')">6</button>
			</div>
			<div class="digitBtn">
				<button value="1" v-on:click="getNumber('1')">1</button>
				<button value="2" v-on:click="getNumber('2')">2</button>
				<button value="3" v-on:click="getNumber('3')">3</button>
			</div>
			<div class="digitBtn">
				<button value="0" v-on:click="getNumber('0')">0</button>
			</div>
		</div>

		<div class="right">
			 <div class="operatorBtn">
				<button v-on:click="doMath('+')" >+</button>
				<button v-on:click="doMath('-')" >-</button>
			</div>
			<div class="operatorBtn">
				<button v-on:click="doMath('*')">*</button>
				<button v-on:click="doMath('/')">/</button>
			</div>
			<div class="operatorBtn">
				<button v-on:click="squere">x2</button>
				<button v-on:click="squereRoot('√')" v-if="negativeNum">√</button>
			</div>
			<div>
				<button class="clearBtn" v-on:click="clear">C</button>
				<button v-on:click="getResult" class="equal">=</button>
			</div>
		</div>
</div>
  <div>History {{ history }}</div>
  <div class="howToUse">
    How to use this calculator:
    <ol>
      <li><em>Calculator Vue.js</em> is always right.</li>
      <li>For your own safety we higly recommend to use only number buttons.</li>
      <li>Function for "square" and "square root" works only with simple equation. Please, don't make it complicated!</li>
      <li>If you are using <em>Calculator Vue.js</em> e.g. for your tax, we recommend to use another calculator. </li>
    </ol>

  </div>
</div>
</template>

<script>
    export default{

    name: 'calcWrap',
    data: function(){
      return{
				current: '',
				saved:'',
        result: '',
        showCurrResult: '',
        placeholder: 0,
        operator:'',
        lastOperator:'',
        history: [],
        negativeNum: true,
      };
    }, //data
    methods:{
      getNumber:function(num){
        console.log(num);
        this.current += num; //current är sträng
      },
      // ______________Welcome to the world where you can use function eval()________________
			doMath: function(sign){
        //- current sparas till saved
        //- /* har högre prioritet än +-
        this.operator = sign;
        console.log(this.operator);
        if (sign == '+' || sign == '-') {
          if (this.saved !== '') {
            let value;
            if (this.lastOperator === '+') {
              value = Number(this.saved) + Number(this.current);
              console.log(value);
            } else if (this.lastOperator === '-') {
              value = Number(this.saved) - Number(this.current);
            } else if (this.lastOperator === '/') {
              value = Number(this.saved) / Number(this.current);
            } else if (this.lastOperator === '*') {
              value = Number(this.saved) * Number(this.current);
            }
            this.saved = value;
            this.current = '';
            this.lastOperator = sign;
            console.log(this.lastOperator);
         }else{
           this.lastOperator = sign;
           this.saved = this.current;
           this.current= '';
         }
         //end of plus/minus sign
       }else if(sign == '*' || sign == '/'){

         if (this.saved !== '') {
           let value;
           if (this.lastOperator === '+') {
             value = Number(this.saved) + Number(this.current);
             console.log(value);
           } else if (this.lastOperator === '-') {
             value = Number(this.saved) - Number(this.current);
           } else if (this.lastOperator === '/') {
             value = Number(this.saved) / Number(this.current);
           } else if (this.lastOperator === '*') {
             value = Number(this.saved) * Number(this.current);
           }
           this.saved = value;
           this.current = '';
           this.lastOperator = sign;
           console.log(this.lastOperator);
       }
       else{
         this.lastOperator = sign;
         this.saved = this.current;
         this.current= '';
       }
     } //end of */

        // if(this.operator === "+") {
        //      console.log('blablabla');
        //      console.log(this.saved);
        //   }
        //   else if(this.operator === "-") {
        //     this.saved = this.saved - this.current;
        //   }
        //   else if(this.operator === '*') {
        //     this.current = this.current * this.value
        //   }
        //   else if(this.operator === '/') {
        //     this.current = this.current / this.value
        //   }
          // this.saved = this.current;
			},

      getResult: function(val){
        if (this.saved !== '') {
          let value;
          if (this.lastOperator === '+') {
            value = Number(this.saved) + Number(this.current);
            console.log(value);
          } else if (this.lastOperator === '-') {
            value = Number(this.saved) - Number(this.current);
          } else if (this.lastOperator === '/') {
            value = Number(this.saved) / Number(this.current);
          } else if (this.lastOperator === '*') {
            value = Number(this.saved) * Number(this.current);
          }
          this.result = value;
        }
        this.current = '';
        // this.saved = this.result;
        this.saved = '';

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
        }
      },//end of getResult
      squere: function(){
        console.log(parseInt(this.saved));
        this.saved= Math.pow(this.current, 2);
        console.log('square is ', this.saved);
      },
      squereRoot: function(root){
        console.log(parseInt(this.current));
        this.saved= Math.sqrt(this.current);
        console.log(this.saved);
      },
			clear:function(event){
				this.current = '';
				this.result = '';
        this.placeholder = '0';
        this.saved='';
        this.showCurrResult= '';
        this.negativeNum = true;
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
    justify-content: space-between;
    margin:0;
    padding: 15px;
    text-align: center;
    width: 350px;
    height: auto;
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
    margin-bottom: 10px;
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
  .howToUse{
    background-color: #84B9EF;
    border: 1px solid #FFFFFF;
    margin:10px;
    text-align:left;
  }

</style>
