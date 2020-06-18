<template>
  <div id="app">
       <h3 class="text-primary text-center my-3  ">{{name}}</h3>
      <h6 class=" text-center my-3 " :class="ObjectClass">Montant : {{montant}}</h6>

      <div class="row">
           <div class="col-md-8 mx-auto ">
               <div class="card ">
                   <div class="card-body bg-ligh m-auto">
                       <div class="form-inline">
                           <div class="form-group">
                               <input v-model="data.libelle" class="form-control mr-2" type="text" placeholder="Libelle">
                               <input  v-model="data.prix" class="form-control mr-2" type="number" placeholder="Montant">
                               <button class="btn btn-sm btn-success mr-2  " @click="addGains">
                                   <i class="fa fa-plus-square"></i>
                               </button>
                               <button class="btn btn-sm btn-danger mr-2 " @click="addDeponses">
                                   <i class="fa fa-minus"></i>
                               </button>
                           </div>
                       </div>
                   </div>
               </div>
           </div>
       </div>
       <div class="row my-4">
           <div class=" col-md-6 col-sm-12">
               <Gains :bus="bus" :data="data" @gainsAdded="gainsAdded" @removeGai="removeGai" ></Gains>
           </div>
           <div class=" col-md-6 col-sm-12">
               <Deponses :bus="bus" :data="data" @deponsesaAdded="deponsesaAdded" @removeDep="removeDep" ></Deponses>
           </div>
       </div>
  </div>
</template>

<script>
import Gains from "@/components/Gains";
import Deponses from "@/components/Deponses";
import Vue from 'vue';

export default {
  name: 'App',
  data(){
    return{
        bus:new Vue(),
        name:" Gestion De Depenses ",
        data: {libelle:'',prix:''},
        montant:0,
        positif : true
    }
  },
  components:{
    Gains,Deponses
  },
  methods:{
      addDeponses(){
            if (this.data.prix.length && this.data.libelle.length)
                this.bus.$emit('addDeponse');
        },
      deponsesaAdded(){
            this.montant-= parseInt(this.data.prix);
            if(this.montant >= 0)this.positif=true;
            else this.positif=false;
            this.data = {};
      },
      addGains(){
          if (this.data.prix.length && this.data.libelle.length)
              this.bus.$emit('addGain');
      },
      gainsAdded(){
          this.montant += parseInt(this.data.prix);
          if(this.montant >= 0)this.positif=true;
            else this.positif=false;
            this.data = {};
      },
      removeDep(dep){
          this.montant += parseInt(dep.prix);
          if(this.montant >= 0)this.positif=true;
          else this.positif=false;

      },
      removeGai(gai){
          this.montant -= parseInt(gai.prix);
          if(this.montant >= 0)this.positif=true;
          else this.positif=false;
      },
  },
    computed : {
        ObjectClass (){
            return  !this.positif ? 'text-danger':'text-success';
        }
    }
}
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  