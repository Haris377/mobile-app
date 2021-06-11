<template>
  <nb-container>
    <nb-content class="content">
      <image 
         :style="{width:70, height:70, marginLeft:8}"
          :source="require('../assets/avatar.png')"
        ></image>
      <text class="heading2">Enter Your Name</text>
         <TextInput
            class="name" 
            label="First Name"
            mode="outlined"
            v-model="firstName"
            :error="isError1"
        />
         <HelperText v-if="isError1" type="error" visible>
            First Name is Required!
          </HelperText>
         <TextInput
            class="name"
            label="Last Name"
            mode="outlined"
            v-model="lastName"
            :error="isError2"
        />
         <HelperText v-if="isError2" type="error" visible>
            Last Name is Required!
          </HelperText>
            <nb-button :disabled="isDisabled" class="btn" :on-press="next"><nb-text class="text">Next</nb-text></nb-button>
    </nb-content> 
  </nb-container>
</template>


<style>
/* .input{
  border-width: 1;
  border-color: rgb(0, 0, 9);
} */
.content{
  margin: 20px;
  margin-top: 50px;
}
.heading1{
  font-size: 38px;
}
.heading2{
  font-size: 28px;
  margin-top: 10px;
  margin-bottom: 15px;
  margin-left: 10px;
}
.text{
  font-size: 20px;
}
.btn{
  margin-top: 25px;
  margin-left: 72%;
  border-radius: 10px;
}
.name{
  margin: 10px;
  color:black;
  border-radius: 30px;
}
</style>

<script>
//import axios from "axios";
import { TextInput, HelperText } from 'react-native-paper';

export default {
    components: {
    TextInput,
    HelperText
  },
  data(){
    return{
     firstName: '',
     lastName: '',
     isDisabled:false,
     isError1:false,
     isError2:false
    }
  },
 props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    next(){
      if(this.firstName.length == 0 || this.firstName.length < 3){
        this.isError1 = true;
      }
      else{
        this.isError1 = false;
      }
      if(this.lastName.length == 0 || this.lastName.length < 3){
        this.isError2 = true;
      }
      else{
        this.isError2 = false;
      }
      if(this.isError1 == false && this.isError2 == false){
          this.navigation.navigate('AccountInfo');
      }
    },
    // onClick(){
    //   if(this.firstName.length != 0 && this.lastName.length != 0){
    //     this.isDisabled = false;
    //   }
    // }
  },
};
</script>
