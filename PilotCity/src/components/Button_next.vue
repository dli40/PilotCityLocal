<template>
    <div>
    <button type="button"  @click="goforward" class="btn btn-secondary btn-lg" id="the_best_next_button" disabled>Next</button>
    <button type="button" @click="goback" class="btn btn-secondary btn-lg" id="the_best_prev_button" >Back</button>
    </div>
</template>

<script>
import { bus } from '../main'
export default {
    name: "Button_next",
    data(){
        return{
            role: null,
            step: 0,
        }
    },
    methods:{
        grabDataFromForm: function(){
            switch(this.step){
                case 1:
                    if (this.role == 'teacher')
                        bus.$emit('grab_data', { step: 'story_teacher'});
                    if (this.role  == 'employer')
                        bus.$emit('grab_data', { step: 'story_employer'});
                break ;
                case 2:
                    if (this.role  == 'teacher')
                        bus.$emit('grab_data', { step: 'story_teacher_address'});
                    if (this.role  == 'employer')
                        bus.$emit('grab_data', { step: 'story_employer_address'});
                break ;
                case 3:
                    if (this.role  == 'teacher')
                        bus.$emit('grab_data', { step: 'teacher_class'});
                    if (this.role  == 'employer')
                        bus.$emit('grab_data', { step: 'employer_sector'});
                break ;
                case 4:
                    if (this.role  == 'teacher')
                        bus.$emit('grab_data', { step: 'teacher_ptype'});
                    if(this.role == 'employer')
                        bus.$emit('grab_data', {step: 'employer_industry'})
                break ;
                case 5:
                    if (this.role  == 'teacher')
                        bus.$emit('grab_data', { step: 'teacher_skills'});
                    if(this.role == 'employer')
                        bus.$emit('grab_data', {step: 'employer_solution_type'})
                break ;
                case 6:
                    if (this.role  == 'teacher')
                        bus.$emit('grab_data', { step: 'teacher_industry'});
                    if(this.role =='employer')
                        bus.$emit('grab_data', {step: 'employer_solution_keywords'})
                break ;
                case 7:
                    if(this.role == 'employer')
                        bus.$emit('grab_data', {step:'employer_flock'})
            }
        },
        increment: function(){
            bus.$emit('move', {dirct: 'right', step: this.step++});
            if (this.step == 6 && this.role=='teacher')
                document.getElementById("the_best_next_button").innerHTML = 'Finish';
            if(this.step == 7)
                document.getElementById("the_best_next_button").innerHTML='Finish';
        },
        goforward: function(){
            document.getElementById('the_best_prev_button').style.display = "block";
            $('#class_picker').addClass('fadeOut');
            setTimeout(() => {
                $('#class_picker').hide();
            }, 100);
            if (this.step == 0){
                bus.$emit('move', {dirct: 'right', step: this.step++});
                return ;
            }
           
            this.grabDataFromForm();
            setTimeout(() => {}, 1500);
        },
        goback: function(){
            if (this.step > 1){}
                bus.$emit('move', {dirct: 'left', step: --this.step});
            document.getElementById("the_best_next_button").innerHTML = 'Next'
        }
    },
    created(){
        var self = this;
        bus.$on('pickedRole', function(role){
            document.getElementById('the_best_next_button').disabled = false;
            self.role = role;
        });
        bus.$on('validated', ()=> { 
            if (this.step == 6 && this.role=='teacher'){
                $('#thankyou-modal').modal('show');
                bus.$emit('submit');
                return ;
            }    
            if(this.step == 7 && this.role=='employer') {
                $('#employer-thankyou-modal').modal('show');
                bus.$emit('submit');
                return;
            }
        
        self.increment() });
    }
}
</script>

<style>
#the_best_next_button{
    width: 150px;
    position: fixed;
    bottom: 5vh;
    right: 5vw; 
    font-weight: bold;
    font-color: rgb(222, 223, 224);
    border-radius: 50px;
    background-color:rgb(220, 221, 222);
    border-color:rgb(220, 221, 222);
}   

#the_best_next_button:hover {
    width: 150px;
    position: fixed;
    bottom: 5vh;
    right: 5vw; 
    font-weight: bold;
    border-radius: 50px;
    font-color: rgb(222, 223, 224);
    background-color:#404041;
    border-color:#404041;
} 

#the_best_prev_button{
    display: none;
    width: 150px;
    position: fixed;
    bottom: 5vh;
    left: 5vw; 
    font-weight: bold;
    font-color: rgb(222, 223, 224);
    border-radius: 50px;
    background-color:rgb(220, 221, 222);
    border-color:rgb(220, 221, 222);
}

#the_best_prev_button:hover{
    display: none;
    width: 150px;
    position: fixed;
    bottom: 5vh;
    left: 5vw; 
    font-weight: bold;
    font-color: rgb(222, 223, 224);
    border-radius: 50px;
    background-color:#404041;
    border-color:#404041;

}
</style>
