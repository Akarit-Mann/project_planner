<template>
  <div class="project" :class="{complete:project.complete}">
    <div class="flexbox">
        <div>
            <h2  @click="showDetail =! showDetail">{{project.title}}</h2>
        </div>
        <div>
            <div class="fa-solid" @click="deleteProject">
                <i class="fa-solid fa-trash-can"></i>
            </div>
            <router-link :to="{name:'editProject',params:{id:project.id}}">
                <div class="fa-solid" >
                    <i class="fa-solid fa-pen-to-square"></i>
                </div>
            </router-link>
            <div class="fa-solid" @click="completeProject">
                <i class="fa-solid fa-check"></i>
            </div>
        </div>
    </div>

    <p v-if="showDetail===true">{{project.detail}}</p>
  </div>
</template>

<script>
export default {
    props:['project'],
    data() {
        return {
            showDetail:false,
            api:" http://localhost:3000/projects/"
        }
    },
    methods: {
        deleteProject(){
           let deleteRoute = this.api+this.project.id;

           fetch(deleteRoute,{method:"DELETE"})
           .then(()=>{
            this.$emit("delete",this.project.id)
           })
           .catch((err)=>{
            console.log(err)
           })

        },
        completeProject(){
            let completUpdateProject = this.api+this.project.id;
            fetch(completUpdateProject,{
                method:"PATCH",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify(
                    {
                        "complete":!this.project.complete
                    }
                )
            })
            .then(()=>{
                this.$emit("complete",this.project.id)
            })
            .catch((err)=>{
                console.log(err)
            })
        }
    },
}
</script>

<style scoped>

   .project{
        padding: 20px;
        background-color: #F2F2F2;
        margin: 10px;        border-left: 5px solid red;
        border-radius: 5px;
    }
    h2{
        color: indigo;
        user-select: none;
        cursor: pointer;
    }
    .flexbox{
        display: flex;
        justify-content: space-between;
        align-items: center;    }
    .fa-solid{
        margin-left: 10px;
        font-size: 20px;
        transition: all 0.4s ease;
        cursor: pointer;    }
    .fa-solid:hover{
        color:#3399 ;
    }
    .complete{
        border-left:5px solid rgb(46, 225, 46);
    }

</style>