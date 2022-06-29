<template>
    <div class="image">
                      <div class="image__body">
                        <img class="image__itself" src="../assets/img/orc.png" alt="orc and knight" >
                        <div class="image__purple1"></div>
                        <div class="image__purple2"></div>
                        <div v-on:click="closer" class="image__croos croos">
                            <div class="croos__body">
                              <div class="croos__bar1"></div>
                              <div class="croos__bar2"></div>
                    </div>
        </div>
        </div>         
    </div>
</template>



<script>
export default {
  name: 'ImagePart',
 methods: {
        closer(e) {
console.log(e.target.closest('.popup'));
e.target.closest('.popup').classList.remove('open')

        }
    }
}

</script>

<style>
.image {
  max-width: 581px;
  max-height: 502px;
  border-bottom-right-radius: 8px;
  overflow: hidden;
}

.image__body {
  position: relative;
}

.image__itself {
  position: relative;
  z-index: 10;
}

.image__purple1 {
  width: 224px;
  height: 887.96px;
  background-color: #C24DFE;
  position: absolute;
  left: 0;
  top: 0;
  transform: rotate(-14deg) translate(187px, 10px);
  -webkit-transform: rotate(-14deg) translate(187px, 10px);
  -moz-transform: rotate(-14deg) translate(187px, 10px);
  -ms-transform: rotate(-14deg) translate(187px, 10px);
  -o-transform: rotate(-14deg) translate(187px, 10px);
}

.image__purple2 {
  width: 300px;
  height: 800px;
  background-color: #C24DFE;
  position: absolute;
  right: 0;
  top: 0;
  transform: rotate(-12deg) translate(12px, -653px);
  -webkit-transform: rotate(-12deg) translate(12px, -653px);
  -moz-transform: rotate(-12deg) translate(12px, -653px);
  -ms-transform: rotate(-12deg) translate(12px, -653px);
  -o-transform: rotate(-12deg) translate(12px, -653px);
}

.image__croos {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 40;
  width: 15px;
  height: 15px;
  margin-top: 9px;
  margin-right: 9px;
  cursor: pointer;
}

.croos__body {
  position: relative;
  width: 15px;
  height: 15px;
}

.croos__bar1 {
  background-color: #2F3639;
  width: 14.14px;
  height: 1px;
  position: absolute;
  transform: translate(0px, 7px) rotate(-45deg);
  -webkit-transform: translate(0px, 7px) rotate(-45deg);
  -moz-transform: translate(0px, 7px) rotate(-45deg);
  -ms-transform: translate(0px, 7px) rotate(-45deg);
  -o-transform: translate(0px, 7px) rotate(-45deg);
  border-radius: 5px;
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  -ms-border-radius: 5px;
  -o-border-radius: 5px;
}

.croos__bar2 {
  background-color: #2F3639;
  width: 14.14px;
  height: 1px;
  position: absolute;
  transform: translate(0px, 7px) rotate(45deg);
  -webkit-transform: translate(0px, 7px) rotate(45deg);
  -moz-transform: translate(0px, 7px) rotate(45deg);
  -ms-transform: translate(0px, 7px) rotate(45deg);
  -o-transform: translate(0px, 7px) rotate(45deg);
  border-radius: 5px;
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  -ms-border-radius: 5px;
  -o-border-radius: 5px;
}


</style>