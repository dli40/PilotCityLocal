<template>
    <div class="container-fluid mt-5 mx-auto Raleway">
        <h4 class="font-weight-bold">
            <div>
                <h2 class="label-title-pink">What's your story?</h2>
            </div>
        <div class="d-flex flex-row justify-content-center">
            <div class="p-2 align-self-center">
                <p class="paragraph_setup_gray">My name is</p>
            </div>
            <div class="p-2 align-self-start">
                <input type="text" placeholder="First Name" class="input-field-pink" v-model="first_name" >
            </div>
            <div class="p-2 align-self-start">
                <input type="text" placeholder="Last Name" class="input-field-pink" v-model="last_name"> 
            </div>
        </div>
        <div class="d-flex flex-row justify-content-center mr-5" >
            <div class="p-2 align-self-center">
                <p class="paragraph_setup_gray">and I am a teacher at</p>
            </div>
            <div class="p-2 align-self-start">
                <input type="text" placeholder="School Name" class="input-field-pink" v-model="school_name">
            </div>
            <div class="p-2 align-self-center">
                <p class="paragraph_setup_gray">of the </p>
            </div>
        </div>
        <div class="d-flex flex-row justify-content-center">
            <div class="p-2 align-self-start">
                <input type="text" placeholder="School District" class="input-field-pink" v-model="school_district">
            </div>
            <div class="p-2 align-self-center">
                <p class="paragraph_setup_gray">My phone number is</p>
            </div>
            <div class="p-2 align-self-start">
                    <input type="number" placeholder="Mobile Number" class="input-field-pink" v-model="phone">
            </div>
        </div>
        </h4>
    </div>
</template>

<script>
import { bus } from '../../../main'
import { Prompter } from '../../../main'

export default {
    name:"w_story",
    data() {
        return {
            first_name:null,
            last_name:null,
            school_name:null,
            school_district:null,
            phone:null
        }
    },
    methods:{
      /** delete this skip when in production */
        skip: function(){
            bus.$emit('validated');
        } 
    },
    created(){
        var self = this;
        bus.$on('grab_data', function(obj){
            if (obj.step != 'story_teacher')
                return ;
            if (self.first_name && self.last_name && self.school_name && self.school_district && self.phone){
                var obj = {};
                obj['paragraph_setup_gray'] = {
                    first_name: self.first_name,
                    last_name: self.last_name,
                    school_name: self.school_name,
                    school_district: self.school_district,
                    phone: self.phone
                }
                bus.$emit('form_completed', obj);
                bus.$emit('validated');
                return ;
            }
            else
                Prompter().failed("You're missing a few things","Hey there,");
        });
    }
}
</script>

<style scoped>

.paragraph_setup_gray{
    font-family: "Raleway";
    font-style:Italic;
    font-size: 25px;
    color: #dbdcde;
    margin-top:10px;
}

input:focus{
    outline: none;
}


.input-field-pink {
        font-family: "Raleway";
        font-weight:300;
        font-style: Italic;
        background-color: #eca0be;
        color: white;
        border-radius: 50px;
        font-size:20px;
        height: 50px;
        width: 250px;
        text-align: center;
        padding-left: 30px;
        padding-right:30px;
        margin-left:5px;
        margin-right:5px;
        border-color: transparent;
        text-transform: capitalize;
}

.input-field-pink::placeholder {
    color:white;
    font-weight:500i;
    font-size:20px;
    text-align: center;

}

.input-field-pink::placeholder:focus {
    color:#eca0be !important;
    border:transparent;

}

.label-title-pink {
    text-align: center;
    font-family: "Raleway";
    font-style: Italic;
    font-weight:700;
    font-size:30px;
    color:#eca0be;
    margin-bottom:50px;
    margin-top:70px;
}

</style>
