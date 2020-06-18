<template>
    <div>
        <h3 class="text-info text center "  > Deponses </h3>
        <hr>
        <ul class="list-group" v-for="(dep ,index) in depenses " :key="index">
            <li class="list-group-item ">{{ dep.libelle}}  {{dep.prix}} MAD
              <span class="ml-4 btn btn-sm btn-danger float-right" @click="remove(dep,index)"><i class="fas fa-minus-square"></i></span>

            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "Deponses",
        props :['bus','data'],
        data(){
            return {
                depenses:[]
            }
        },
        methods:{
            addDepenses(){
                this.depenses.push(this.data);
                this.$emit('deponsesaAdded');
            },
            remove (dep,index){
                this.depenses.splice(index,1);
                this.$emit('removeDep',dep);
            }
        },
        mounted () {
            this.bus.$on('addDeponse',this.addDepenses)  ;

        }
    }
</script>

<style scoped>

</style>