<template>
    <div class= "container-fluid" id="canvas">
        <div class= "justify-content-left align-items-center">
            <div class="class d-flex col-12 mt-5">
                <h2 id = "title">Connecting classrooms to the big bad world. </h2>
            </div>
            <div class="class d-flex flex-row mb-auto mr-auto ml-5">
                <button type="button" class="btn btn-primary mr-4" id="button_forteachers" @click="open_modal">  For Teachers </button>
                <button type="button" class="btn btn-primary" id="button_foremployers" @click="open_modal">  For Employers </button>
            </div>
        </div> 
</div>
</template>
<script>

import w_tymod from '@/components/wizard/teacher/w_tymod'
export default {
    name: "Index",
    data() {
        return{
            
        }
    },
    methods:{
        open_modal: function(){
            $('#signup-modal').modal('show');
        }
    }
}
</script>
<style>
#title {
        font-family: "Raleway";
        font-weight: 700;
        color: white;
        font-size: 7vh;
        margin-left:30px;
        margin-top:190px;
        margin-bottom:40px;
    }
#button_forteachers{
        font-family: "Raleway";
        font-size: 20px;
        background-color: #eca0be;
        color: #ffffff;
        font-weight: 700;
        border-radius: 50px;
        height: 45px;
        width: 250px;
        text-align: center;
        border-color: transparent;
        padding-left:30px;
        padding-right:30px;
    }
    
#button_foremployers:hover{
        border: solid 1px white;
    }

#button_foremployers {
        font-family: "Raleway";
        font-size: 20px;
        font-weight: 700;
        background-color: #ae90b0;
        stroke: #ae90b0;
        color: #ffffff;
        border-radius: 50px;
        height: 45px;
        width: 250px;
        padding-left:30px;
        padding-right:30px;
        text-align: center;
        border-color: transparent;
    }
    #button_forteachers:hover{
        border: solid 1px white;
    }
    #canvas{
        height:calc(100% - 65px);
        width: 100%;
        position: absolute !important;
        background: url('../assets/header.jpg') no-repeat;
        background-size:cover;
    }
  
</style>
