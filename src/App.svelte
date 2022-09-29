<script lang="ts">
import { onMount } from 'svelte';

   
	
  let cardName :HTMLInputElement;
  let cardNumber :HTMLInputElement;


  function showSuccess(input){
  const formControl = (input.parentElement)
    formControl.className = 'good';
    const small = formControl.querySelector('#small').innerText = ''

  }
  function showError(input,text){
    const formControl = (input.parentElement)
    formControl.className = 'error';
    const small = formControl.querySelector('#small').innerText = text

  }
	function handleSubmit(e) {
    
    checkCardName(cardName)
    checkCardNumber()
}




function checkCardName(cardName){
 let re = /^[a-z][^0-9\+~!@#$%^&*()_=+-./[\]\{\}\|""'';:<,>.?\\92]+$/gi
 if(re.test(cardName.value.trim())){
    showSuccess(cardName,'Good')
  }else if(cardName.value.trim() === '' ){
    showError(cardName,'Name is required')
  }else{
    showError(cardName,'Name is badly Format')
  }
}
function checkCardNumber(){
  //  let regix =  /^(?:(4[0-9]{12}(?:[0-9]{3})?)|(5[1-5][0-9]{14})|(6(?:011|5[0-9]{2})[0-9]{12})|(3[47][0-9]{13})|(3(?:0[0-5]|[68][0-9])[0-9]{11})|((?:2131|1800|35[0-9]{3})[0-9]{11}))$/

  if(cardNumber.value.trim() == ''){
    showError(cardNumber,'Credit Number is required')
  }
   else if (cardNumber.value.length > 15){
     checkCardNumberOnTime()
    showSuccess(cardNumber)

  }
  else{
    showError(cardNumber,' is required')
  }

  // Credit is badly format
}
function checkCardNumberOnTime(){
  cardNumber.value = cardNumber.value.slice(0,18) 
 
     
        if(cardNumber.value.match(/^34|37/)){
          //American Express 15digit
           showSuccess(cardNumber)
         cardNumber.value = cardNumber.value.substring(0,18)
        }if(cardNumber.value.match(/^4/)){
          //visa 16digit
           showSuccess(cardNumber)
          cardNumber.value = cardNumber.value.substring(0,19)

        }
        if(cardNumber.value.match(/^[51-55]/)){
          //mastercard 16digit
           showSuccess(cardNumber)
          cardNumber.value = cardNumber.value.substring(0,19)
        }
         if(cardNumber.value.match(/^6011/)){
          //Discover  15digit
           showSuccess(cardNumber)
          cardNumber.value = cardNumber.value.substring(0,18)
        }
         if(cardNumber.value.match(/^[300-305] | 36 | 38/)){
          //Diners Club   14digit
           showSuccess(cardNumber)
          cardNumber.value = cardNumber.value.substring(0,17)
        }
         if(cardNumber.value.match(/^2131 | 1800/)){
          //JCB    15digit
           showSuccess(cardNumber)
          cardNumber.value = cardNumber.value.substring(0,18)
        }
         if(cardNumber.value.match(/^35/)){
          //JCB    14digit
           showSuccess(cardNumber)
          cardNumber.value = cardNumber.value.substring(0,17)
        }

      
      
     
    if(cardNumber.value.length != ''){
      cardNumber.value = cardNumber.value.replace(/\W/gi,'').replace(/(.{4})/g,"$1 ")
    }
   
}
</script>

<form id="form" on:submit|preventDefault={handleSubmit} action="/" method="GET">
  <div>
    <label >Name</label>
    <input bind:this={cardName}  type="text" > 
     <span  id="small"> </span>
  </div>

  <div>
    <label >Credit Number</label>
    <input bind:this={cardNumber}  on:keyup={checkCardNumberOnTime}  >
     <span  id="small"> </span>
  </div>
  <!-- <p>{checkCardNumber}</p> -->
  <button type="submit">Submit</button>
</form>

<style>
.black{
  border: 1px solid;
}
   
</style>  