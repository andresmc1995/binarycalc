<template>
  <div>
  <b-container class="calc">
    <hr>
  <div class="row">
    <div class="col-3">Decimal</div>
    <div class="col-6">Binary</div>
    <div class="col-2">Append</div>
    <div class="col-1">Clear</div>
    </div>
  <hr>
  <div class="row">
  <div class="col-3"><nav aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item active" aria-current="page">{{decimal1}}</li>
  </ol>
</nav></div>
  <div class="col-6"><nav aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item active" aria-current="page">{{current}}</li>
  </ol>
</nav></div>
  <div class="col-1"><button type="button" class="btn btn-light btn-large btn-block" @click= "agregarCero">0</button></div>
  <div class="col-1"><button type="button" class="btn btn-dark btn-lg btn-block" @click= "agregarUno">1</button></div>
  <div class="col-1"><button type="button" class="btn btn-success" @click= "clearVisor1">Clear</button></div>
</div>
<hr>
<div class="row">
  <div class="col"><button type="button" class="btn btn-primary btn-lg btn-block" @click= "binAnd">&</button></div>
  <div class="col"><button type="button" class="btn btn-danger btn-lg btn-block" @click= "binOr">|</button></div>
  <div class="col"><button type="button" class="btn btn-warning btn-lg btn-block" @click= "binXor">^</button></div>
  </div>
<hr>
<div class="row">
  <div class="col-3"><nav aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item active" aria-current="page">{{decimal2}}</li>
  </ol>
</nav></div>
  <div class="col-6"><nav aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item active" aria-current="page">{{current2}}</li>
  </ol>
</nav></div>
  <div class="col-1"><button type="button" class="btn btn-light btn-large btn-block" @click= "agregarCero2">0</button></div>
  <div class="col-1"><button type="button" class="btn btn-dark btn-lg btn-block" @click= "agregarUno2">1</button></div>
  <div class="col-1"><button type="button" class="btn btn-success" @click= "clearVisor2">Clear</button></div>
</div>
<hr>
<div class="row">{{currOp}}</div>
<hr>
<div class="row">
    <div class="col-3">Decimal</div>
    <div class="col-6">Binary</div>
    </div>
    <hr>
<div class="row">
<div class="col-3"><nav aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item active" aria-current="page">{{decRes}}</li>
  </ol>
</nav></div>
  <div class="col-6"><nav aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item active" aria-current="page">{{result}}</li>
  </ol>
</nav></div>
  </div>
<hr>
</b-container>
</div>
  </template>
<script>
export default {
  data()
  {
    return{
      current: '-',
      current2: '-',
      result: '-',
      decRes:'-',
      currOp: '-'
    }
  },
  computed:{
    decimal1: {
      get: function(){
        if(this.current=='-')
        return '-';
        else
        return parseInt(this.current, 2);
      }
    },
    decimal2: {
      get: function(){
        if(this.current2=='-')
        return '-';
        else
        return parseInt(this.current2, 2);
      }
     }
    },
  watch:{
   current:function(){
     this.decRes='-';
   },
   current2:function(){
     this.decRes='-';
   },
   result:function(){
     if(this.result!=='-')
     this.decRes=parseInt(this.result, 2);
   }
  },
  methods:{
    agregarCero(){
      if(this.current==='-'){this.current='0';}
      else{
        if(this.current.length<=30)
        this.current+='0';
        }
      this.result='-';
      this.currOp='-';
    },
    agregarUno(){
      if(this.current==='-'){this.current='1';}
      else{
        if(this.current.length<=30)
        this.current+='1';}
      this.result='-';
      this.currOp='-';
    },
     agregarCero2(){
     if(this.current2==='-'){this.current2='0';}
     else{
       if(this.current2.length<=30)
       this.current2+='0';}
     this.result='-';
     this.currOp='-';
    },
    agregarUno2(){
      if(this.current2==='-'){this.current2='1';}
      else{
        if(this.current2.length<=30)
        this.current2+='1';}
      this.result='-';
      this.currOp='-';
    },
    binAnd(){
      let aux='';
      //veo si no ya hay 0 0 1 en los dos visores
      if(this.current==='-' || this.current2==='-')
      {
        return;
      }
      //termino la vista
      //empieza el checkeo
      let min=Math.min(this.current.length,this.current2.length);
      let max=Math.max(this.current.length,this.current2.length);
      let dif=max-min;
      if(this.current.length<max){
        let aux='';
        for(let i=0;i<dif;i++){
          aux+='0';
        }
        aux+=this.current;
        this.current=aux;
      }else{
        let aux='';
        for(let i=0;i<dif;i++){
          aux+='0';
        }
        aux+=this.current2;
        this.current2=aux;
      }
      //termina el checkeo
      for(let i =0; i<this.current.length; i++){
        if(this.current[i]===this.current2[i])
        {
          aux+=this.current[i];
        }
        else{
          aux+='0';
        }
      }
    this.result=aux;
    this.currOp='The result of the AND operation between the two numbers is: ';
    },
    binOr(){
      let aux='';
      //veo si no ya hay 0 0 1 en los dos visores
      if(this.current==='-' || this.current2==='-')
      {
        return;
      }
      //termino la vista
      //empieza el checkeo
      let min=Math.min(this.current.length,this.current2.length);
      let max=Math.max(this.current.length,this.current2.length);
      let dif=max-min;
      if(this.current.length<max){
        let aux='';
        for(let i=0;i<dif;i++){
          aux+='0';
        }
        aux+=this.current;
        this.current=aux;
      }else{
        let aux='';
        for(let i=0;i<dif;i++){
          aux+='0';
        }
        aux+=this.current2;
        this.current2=aux;
        
      }
      //termina el checkeo
       for(let i =0; i<this.current.length; i++){
        if(this.current[i]==='0' && this.current2[i]==='0')
        {
          aux+='0';
        }
        else{
          aux+='1';
        }
      }
    this.result=aux;
    this.currOp='The result of the OR operation between the two numbers is: ';
    },
    binXor(){
      let aux='';
      //veo si no ya hay 0 0 1 en los dos visores
      if(this.current==='-' || this.current2==='-')
      {
        return;
      }
      //termino la vista
      //empieza el checkeo
      let min=Math.min(this.current.length,this.current2.length);
      let max=Math.max(this.current.length,this.current2.length);
      let dif=max-min;
      if(this.current.length<max){
        let aux='';
        for(let i=0;i<dif;i++){
          aux+='0';
        }
        aux+=this.current;
        this.current=aux;
      }else{
        let aux='';
        for(let i=0;i<dif;i++){
          aux+='0';
        }
        aux+=this.current2;
        this.current2=aux;
      }
      //termina el checkeo
       for(let i =0; i<this.current.length; i++){
        if(this.current[i]!==this.current2[i])
        {
          aux+='1';
        }
        else{
          aux+='0';
        }
      }
    this.result=aux;
    this.currOp='The result of the XOR operation between the two numbers is: ';
    },
    clearVisor1(){
      this.current='-';
      this.result='-';
      this.currOp='-';
    },
    clearVisor2(){
      this.current2='-';
      this.result='-';
      this.currOp='-';
    }
  }
}
</script>
<style scoped>
.calc{
  font-size: 25px;
  width: 1300px;
  margin: 0 auto;
}
.btn{
  font-size: 25px;
}
</style>
