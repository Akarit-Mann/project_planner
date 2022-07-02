<template>
  <h1>EditProject {{id}}</h1>
     <form @submit.prevent="addProject">
    
        <label for="">Project Title</label>
        <input type="text" v-model="title">

        <label for="">Project Detail</label>
        <input type="text" v-model="detail">

        <button @click="updateProject">UpdateProject</button>

   </form>

</template>

<script>
export default {
    props:["id"],
    data() {
        return {
            title:"",
            detail:""
        }
    },
    mounted() {
        fetch("http://localhost:3000/projects/"+this.id)
        .then((res)=>{
            return res.json()
        })
        .then((data)=>{
            console.log()
            this.title = data.title
            this.detail = data.detail
        })
        .catch((err)=>{
            console.log(err)
        })
    },
    methods: {
        updateProject(){
             fetch("http://localhost:3000/projects/"+this.id,
             {
                method:"PATCH",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify(
                    {
                        title:this.title,
                        detail:this.detail
                    }
                )
             })
             .then(()=>{
                this.$router.push("/")
             })
             
             
        }
    },
}
</script>

<style>

</style>