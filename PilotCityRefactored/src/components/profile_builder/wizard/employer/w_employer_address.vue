<template>
   <div class="container p-auto mt-5 pt-5">
        <form class="mt-3" > 
            <div class="form-group-address col-md-10 pl-0 pr-0 justify-content-center">
                <label for="inputAddress">Employer Address</label>
                <input type="text" class="form-control"  placeholder="123 Sesame Street" v-model="employer_data.address.street" @keyup.ctrl="skip">
            </div>
            <div class="form-row justify-content-center" >
                <div class="form-group col-md-6">
                    <label for="inputCity">City</label>
                    <input type="text" class="form-control"  placeholder="Dreamland" v-model="employer_data.address.city">
                </div>
                <div class="form-group col-md-2">
                    <label for="inputState">State</label>
                    <input type="text" class="form-control"  placeholder="NY" v-model="employer_data.address.state">
                </div>
                <div class="form-group col-md-2">
                    <label for="inputZip">Zip</label>
                    <input type="text" class="form-control"  placeholder="12345" v-model="employer_data.address.zip">
                </div>
            </div>

        </form>
        
         <next_button
            route='w_employer_sector'
            :conditions="conditions"
            :collection="collection"
            :pass=pass
            :callback="convert_address_to_coordinate"
            />
        <router-link :to="{ name: 'w_employer_story' }" 
            class="prev_button btn btn-secondary btn-lg">
            Back
        </router-link>
   </div>
</template>

<script>

import { bus } from '@/main'
import { Prompter } from '@/main'
import button from '@/components/profile_builder/wizard/components/button'
import firebase from '@/firebase/init'
import axios from 'axios'
export default {
    name: "w_employer_address",
    data(){
        return {
            employer_data: {
                address: {
                    street: null,
                    city: null,
                    state: null,
                    zip: null,
                },
            },
            collection: ['employers']
        }
    },
    methods:{
        convert_address_to_coordinate(){
            var self = this;
            var link = "https://maps.googleapis.com/maps/api/geocode/json?address="
            var address = this.employer_data.address.street
            + this.employer_data.address.city
            + this.employer_data.address.state;
            address = address.split(' ').join('+');
            var key = "&key=AIzaSyDfuNr3RaCZkituTfoB7b7pR2u2rWuraWE"
            
            return (axios.get(link + address + key));
        }
    },
    components: {
        next_button:button
    },
    computed: {
        conditions(){
            return [this.employer_data]
        },
        pass() {
            return _.every(this.employer_data.address,Boolean)
        }
    },
   created(){
        var self = this
        let data = [self.employer_data]
        firebase.auth().onAuthStateChanged((user) => {
            if(user) {
                const db = firebase.firestore()
                for(let i = 0;i<self.collection.length;i++)
                db.collection(self.collection[i]).doc(user.uid).get().then((doc) => {
                    let obj = doc.data()
                    for (let field in data[i]) {
                        if(obj.hasOwnProperty(field)) {
                            data[i][field]=obj[field]
                        }    
                    }
                })
            }
        })
    }
}
</script>

<style>

.form-group-address{
    margin:auto;
    margin-bottom: 20px;
}
.btn-address-purple{
    border-style: dotted;
    background-color: white;
    border-color: #ae90b0;
    color: #ae90b0;
    border-radius:50px;
    height: 50px;
}

.btn-address-purple:hover, 
.btn-address-purple:active{
    background-color: #ae90b0 !important;
    border-color: #ae90b0  !important;
    color: white;
}
.btn-address-purple:focus{
    outline: none !important;
}
</style>

<style scoped>
label {
    color: #ae90b0;
    font-weight: bold;
    font-size:15px;
    margin-left:15px;
}

input, input:focus{
    border-radius: 50px;
    font-size: 18px;
    padding-left:20px;
    font-weight:300;
    font-style:italic;
    font-family: "Raleway";
    background-color: rgb(222, 223, 224);
    color: white;
    outline: none !important;
    height: 50px;
    border-color: #dbdcde;
    box-shadow: none !important;
}
input::placeholder { 
    font-weight:300;
    color: white;
    font-style:italic;

}

 input:focus, select:focus, .dropdown-class:focus{
    border-color: #c6c8ca !important;
 }
 @media only screen and (max-width: 700px){
#the_best_next_button {
    position: absolute;
  bottom: 35px;
  right: 15px;
  height: 45px;
  width: 165px;
  font-size: 2.5vh;
  
}
}
</style>
 
 