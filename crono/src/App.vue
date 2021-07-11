<template>
  <div id="app">
    <img class="img" src="./assets/cronometro.png"/>
    <a class="timer">{{numero}}</a>

    <div class="areaBtn">
      <button class="botao" @click="vai">{{botao}}</button>
      <button class="botao" @click="limpar">LIMPAR</button>
    </div>

    <div class="list" v-show="historico.length > 0" >
      <ul>
        <li v-for="item in historico" :key="item"> TEMPO REGISTRADO EM: {{item}} </li>
      </ul>
      <button class="btnClean" @click="historico =[]">Limpar historico</button>
    </div>

  </div>
</template>

<script>
 
export default {
  name: 'App',
  data(){
    return{
      numero:0,
      botao:'VAI',
      timer:null,
      ms:0,
      ss:0,
      mm:0,
      hh:0,
      
      historico: []
    }
  },
  methods:{
    vai(){
      
      if(this.timer != null){
        //SE O TIMER ESTIVER RODANDO
        clearInterval(this.timer)
        this.timer = null
        this.botao ='VAI'

        if(this.ms !== 0){
          this.historico.push(this.numero);
        }
      }else{
        //SE O TIMER NÃO ESTIVER RODANDO
        this.timer = setInterval(()=>{
           this.rodarTimer();
        },10);

        this.botao = 'PAUSAR ';
      }

    },
    limpar(){

      if(this.timer !== null){
        clearInterval(this.timer);
        this.timer = null;
      }

      this.ss=0;
      this.hh=0;
      this.mm=0; 
      this.ms=0;
      
      this.numero =0;
      this.botao='VAI';
      this.historico = []
    },

    rodarTimer(){
        this.ms++;

        if(this.ms == 99){
          this.ms=0;
          this.ss++;
          
        }

        if(this.ss == 59){
          this.ss=0;
          this.mm++;
          
        }

        if(this.mm ==59){
          this.mm=0;
          this.hh++;
        }
        

      let format = (this.hh<10?'0'+this.hh : this.hh) + ':'
      + (this.mm <10 ?'0'+ this.mm : this.mm)+ ':'
      + (this.ss <10 ?'0'+ this.ss : this.ss) + ','
      + (this.ms <10 ?'0'+ this.ms : this.ms);

      return this.numero = format;

    }
  }
 
}
</script>

<style>
  #app{
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }

  .img{
    width: 45vh ;
    padding-top: 5%;
  }

  .timer{
    color:#ffffff;
    font-size:6vh; 
    
    margin-top: -26vh;
  } 

  .areaBtn{
    display:flex;
    margin: 20vh 0vh 0vh 0vh;
  }

  .botao{
    -webkit-user-select: none;
    -moz-user-select: none;
    width: 20vh;
    background-color: #ffffff;
    font-size: 12pt;
    border:0;
    border-radius: 5px;
    margin: 0 4vh;
    padding: 1vh;
    cursor: pointer;
    
  }

  .botao:hover{
    color:coral;
    background-color: rgba(0, 0, 0, 0.363);
    transition: all 0.3s;
  }

  ul{
    text-align: center;
    padding: 0;
  }

  .list{
    margin-top:1vh
  }

  ul li{
    margin-top: 8px;
    padding: 15px;
    background-color: rgb(70,70,70);
    color: #fff;
    list-style:none;
    font-size: 12pt;
    border-radius: 6px;

  }

  .list button{
    cursor: pointer;
    border: 0;
    background-color: #FFF;
    padding: 8px;
    border-radius: 5px;
    margin-bottom: 12px;

  }

  .btnClean{
    -webkit-user-select: none;
    -moz-user-select: none;
    width: 20vh;
    background-color: #ffffff;
    font-size: 12pt;
    border:0;
    border-radius: 5px;
    margin: 0 4vh;
    padding: 1vh;
    cursor: pointer;
  }

  .btnClean:hover{
    color:coral;
    background-color: rgba(0, 0, 0, 0.363);
    transition: all 0.3s;
  }

</style>
