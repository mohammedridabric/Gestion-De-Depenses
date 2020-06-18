<template>
    <div>
        <h3 class="text-info">Gains </h3>
        <hr>
        <ul class="list-group" v-for="(gas ,index) in gains " :key="index">
            <li class="list-group-item ">{{ gas.libelle}}  {{gas.prix}} MAD
                <span class="ml-4 btn btn-sm btn-danger float-right" @click="remove(gas,index)"><i class="fas fa-minus-square"></i></span>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "Gains",
        props :['bus','data'],
        data(){
            return {
                gains:[]
            }
        },
        methods:{
           addGains(){
               this.gains.push(this.data);
               this.$emit('gainsAdded');
           },
            remove (gai,index){
                this.gains.splice(index,1);
                this.$emit('removeGai',gai);
            }
        },
        mounted () {
            this.bus.$on('addGain',this.addGains)  ;

        }

    }
</script>

<style scoped>

</style>