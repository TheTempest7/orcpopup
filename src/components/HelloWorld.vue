<template>
  <div class="wrapper" >
    <div  class="popUpOpenBtn">
    <button v-on:click="open" class="popUpOpenBtn__btn" type="button">Open Pop-Up</button>
    </div>
    <div id="popup" ref="popuper" class="popup lockPadding ">
                <div class="popup__body ">
                    <form v-on:submit="validation"  action="#" id="form" class="popup__content">
                        <h1 class="popupform__title">10% <span>off</span>  </h1>
                        <h2 class="popupform__title2">your first order </h2>
                        <div class="popup__recktangle"></div>
                        <p class="popup__text">Subscrive to recieve 10% off promocode plus exclusive offers and deals</p>
                <div class="popupform__item">
                    <label for="formEmail" class="popupform__label">Email-adress</label>
                    <input ref="inputEmail" id="formEmail" type="text" name="email" class="popupform__input  __email __req">
                </div>
                <div class="popupform__item">
                  <button type="submit" class="popupform__button">Subscribe!</button>
                    <div class="popupcheckbox">
                        <input v-on:click="checker" ref="chechbox" id="formAgreement"  checked type="checkbox" name="agreement" value="left" class="popupcheckbox__input checked __req ">
                        <label for="formAgreement" class="popupcheckbox__label"><span>I’m agree with privacy policy</span></label>
                    </div>

                </div>
                
                    </form>
                    <Image/>
                </div>
                <div ref="green" class="popup__green">
                  You have successfully subscribed to the newsletter
                </div>
                <div ref="red" class="popup__red">
                  You have already subscribed to the newsletter
                </div>
    </div>
            
  </div>
</template>

<script>
import Image from "./Image.vue";
export default {
    name: "HelloWorld",
    props: {
        msg: String,
        pop:{}
    },

    
    methods: {
        checker(e){
        e.target.classList.toggle('checked');
        }
        ,
        open() {
            const popup = this.$refs.popuper;
            popup.classList.add("open");
        },
        validation(e){
          e.preventDefault();
            function testEmail(inputData){
            let re=/^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
            return re.test(inputData);
          }
          let chechbox=this.$refs.chechbox;
          let arr=chechbox.classList;

          let s=Object.values(arr).filter(i=>(i==='checked'));
          


          
          let inputData=this.$refs.inputEmail.value;
          let currentEmail=localStorage.getItem('emails');


          if(inputData){
            let emailObject=JSON.parse(currentEmail);
            let compare;
            if(emailObject){
                emailObject.forEach(i=>{if(i===inputData){
                compare=true;
            }})
            }
            if(compare===true){
              let red=this.$refs.red;
              red.classList.add('show');
              setTimeout(()=>{
              red.classList.remove('show');
            },4000)
            }
            else{
          if((s[0])&&testEmail(inputData)&&(currentEmail)){
            let emailObject=JSON.parse(currentEmail);
            emailObject.push(inputData);
            localStorage.setItem('emails',JSON.stringify(emailObject));
            let green=this.$refs.green;
            green.classList.add('show');
            setTimeout(()=>{
              green.classList.remove('show');
            },4000)
          }
          else if((s[0])&&testEmail(inputData)&&(!currentEmail)){
          localStorage.setItem('emails',JSON.stringify([inputData]));
            let green=this.$refs.green;
            green.classList.add('show');
            setTimeout(()=>{
              green.classList.remove('show');
            },4000)
          }
         this.$refs.inputEmail.value='';
            }
          }
         
        }
    },
    components: { Image }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.popUpOpenBtn {
  margin: 200px auto;
  display: flex;
  justify-content: center;
}

.popUpOpenBtn__btn {
  width: 212px;
  height: 60px;
  font-family: "Roboto";
  font-style: normal;
  font-weight: 700;
  font-size: 24px;
  line-height: 14px;
  background-color: #C24DFE;
  border-radius: 35px;
  -webkit-border-radius: 35px;
  -moz-border-radius: 35px;
  -ms-border-radius: 35px;
  -o-border-radius: 35px;
  color: aliceblue;
}
body.lock {
  overflow: hidden;
}

.popup {
 /* background-color: rgba(0, 0, 0, 0.5);*/
  margin: 0px auto;
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  z-index: 100;
  opacity: 0;
  visibility: hidden;
  transition: all 0.8s ease 0.3s;
  -webkit-transition: all 0.8s ease 0.3s;
  -moz-transition: all 0.8s ease 0.3s;
  -ms-transition: all 0.8s ease 0.3s;
  -o-transition: all 0.8s ease 0.3s;
}

.popup.open {
  opacity: 1;
  visibility: visible;
}

.popup__body {
height: 502px;
  max-width: 864px;
  display: flex;
  align-items: center;
  justify-content: center;
   background-color: rgb(255, 255, 255);
   margin: 100px auto;
   border-radius: 8px;
   box-shadow: 0px 8px 20px rgba(68, 75, 77, 0.4);
}

.popup__green{
  opacity: 0;
  visibility: hidden;
  width: 200px;
  height: 74px;
  background-color: #215e21;
  position: absolute;
  left: 45%;
    top: 10%;
    z-index: 50;
  font-family: 'Roboto';
    padding: 20px 0px;
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 120%;
    color: #fff;
    text-align: center;
    transition: all 0.8s ease 0.2s;
}
.popup__green.show{
  opacity: 1;
  visibility: visible;
}
.popup__red{ opacity: 0;
  visibility: hidden;
  width: 200px;
  height: 74px;
  background-color: red;
  position: absolute;
  left: 45%;
    top: 10%;
    z-index: 50;
  font-family: 'Roboto';
    padding: 20px 0px;
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 120%;
    color: #fff;
    text-align: center;
    transition: all 0.8s ease 0.2s;}
.popup__red.show{
  opacity: 1;
  visibility: visible;
}
.popup__content {
  display: flex;
  flex-direction: column;
  padding-left: 32px;
  position: relative;
  margin-right: -121px;
}
.popup__content::after {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: rgba(51, 51, 51, 0.9) url(//img/png-clipart-jsplaylist-loading-icon-thumbnail.png) center/50px no-repeat;
  opacity: 0;
  visibility: hidden;
}

.popup__caption {
  font-family: "Playfair Display";
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 131.25%;
  color: #353535;
  flex: 1 1 auto;
}

.popup__item {
  margin-top: 10px;
}

.popup__label {
  font-family: "Source Sans Pro";
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 125%;
  color: #353535;
  white-space: nowrap;
  margin-bottom: 5px;
  display: flex;
}









@media (max-width: 1000px) {
  .popup__content {
    padding: 24px 60px;
  }
}




.popupform__title {
  font-size: 40px;
  font-weight: 700;
  margin-bottom: 30px;
}

.popupform__item {
  margin-bottom: 20px;
}

.popupform__label {
  font-size: 18px;
  margin-bottom: 10px;
  display: block;
}

.popupform__input {
  height: 50px;
  padding: 0px 20px;
  width: 100%;
  border-radius: 5px;
  font-size: 18px;
  transition: box-shadow 0.3s ease 0s;
}

.popupform__input:focus {
  box-shadow: 0 0 15px #42f342;
}

.popupform__input.__error {
  box-shadow: 0 0 15px #f51505;
}

textarea.popupform__input {
  min-height: 120px;
  max-width: 100%;
  resize: vertical;
  padding: 20px;
}
.popupcheckbox.__error .checkbox__label::before {
  box-shadow: 0 0 15px #f51505;
}

.popupcheckbox__input {
  display: none;
}

.popupcheckbox__label {
  cursor: pointer;
  position: relative;
  font-size: 16px;
  line-height: 140%;
  display: inline-flex;
  align-items: center;
  margin-top: 16px;
}

.popupcheckbox__label a {
  color: #2ba12b;
}

.popupcheckbox__label::before {
  content: "";
  flex: 0 0 16px;
  height: 16px;
  background-color: white;
  border: 2px solid #C24DFE;
  border-radius: 4px;
  align-self: flex-start;
  margin-right: 10px;
}

.popupcheckbox__label::after {
  content: "";
  width: 8px;
  height: 8px;
  position: absolute;
  left: 4px;
  top: 4px;
  background-color: #C24DFE;
  border-radius: 1px;
  transform: scale(0);
  transition: transform 0.3s ease 0s;
}

.popupcheckbox__input:checked + .popupcheckbox__label::after {
  transform: scale(1);
}

.popupform__button {
 display: flex;
flex-direction: column;
justify-content: center;
align-items: center;
width: 106px;
height: 40px;
background: #C24DFE;
border-radius: 35px;
font-family: 'Roboto';
font-style: normal;
font-weight: 700;
font-size: 12px;
line-height: 14px;
display: flex;
align-items: center;
text-align: center;
color: #FFF;
}

.popupform__button:hover {
 background: #8734b1;
}

.popupform__button:active {
  top: 3px;
  box-shadow: 0 2px 0 #031b03;
}



.popupform__title {
  font-family: 'Roboto';
font-style: normal;
font-weight: 700;
font-size: 104px;
line-height: 100%;
color: #2F3639;
}
.popupform__title span{
  font-family: 'Roboto';
font-style: normal;
font-weight: 700;
font-size: 24px;
line-height: 100%;
margin-left: -20px;
}
.popupform__title2 {
  font-family: 'Roboto';
font-style: normal;
font-weight: 700;
font-size: 24px;
line-height: 100%;
color: #828688;
margin-bottom: 26px;
}
.popup__recktangle {
  width: 67px;
height: 2px;
background: #C24DFE;
border-radius: 10px;
margin-bottom: 26px;

}
.popup__text {
  font-family: 'Roboto';
font-style: normal;
font-weight: 400;
font-size: 14px;
line-height: 120%;
max-width: 373px;
color: #595E61;
margin-bottom: 40px;
}
.popupform__item {
}
.popupform__label {
  font-family: 'Roboto';
font-style: normal;
font-weight: 700;
font-size: 12px;
line-height: calc(14/12*100%);
color: #828688;
}
.popupform__input {
width: 302px;
height: 40px;
background: #FFFFFF;
border: 1px solid #D5D7D7;
border-radius: 6px;
}
.__email {
}
.__req {
}
.popupform__button {
}
.popupcheckbox {
}
.popupcheckbox__input {
}
.popupcheckbox__label span{
  white-space: nowrap;
  font-family: 'Roboto';
font-style: normal;
font-weight: 500;
font-size: 14px;
line-height: calc(16/14*100%);
color: #595E61;
}

@font-face {
    font-family: 'Roboto';
    src: url('../assets/fonts/Roboto-Black.woff2') format('woff2'),
        url('../assets/fonts/Roboto-Black.woff') format('woff');
    font-weight: 900;
    font-style: normal; 
    font-display: swap;
}

@font-face {
    font-family: 'Roboto';
    src: url('../assets/fonts/Roboto-Bold.woff2') format('woff2'),
        url('../assets/fonts/Roboto-Bold.woff') format('woff');
    font-weight: bold;
    font-style: normal;
    font-display: swap;
}

@font-face {
    font-family: 'Roboto';
    src: url('../assets/fonts/Roboto-Regular.woff2') format('woff2'),
        url('../assets/fonts/Roboto-Regular.woff') format('woff');
    font-weight: normal;
    font-style: normal;
    font-display: swap;
}

@font-face {
    font-family: 'Roboto';
    src: url('../assets/fonts/Roboto-Medium.woff2') format('woff2'),
        url('../assets/fonts/Roboto-Medium.woff') format('woff');
    font-weight: 500;
    font-style: normal;
    font-display: swap;
}

@font-face {
    font-family: 'Roboto';
    src: url('../assets/fonts/Roboto-Light.woff2') format('woff2'),
        url('../assets/fonts/Roboto-Light.woff') format('woff');
    font-weight: 300;
    font-style: normal;
    font-display: swap;
}


</style>
