<template>
   <nb-container>
    <nb-content class="content">
          <view class="item">
          <text class="label">Email</text>
           <TextInput
            class="name" 
            label="name@example.com"
            mode="outlined"
            v-model="email"
            :error="isError1"
            />
            <HelperText v-if="isError1" type="error" visible>
            Email is Required!
          </HelperText>
            <text class="label">Phone Number</text>
            <TextInput
            class="name"
            label="e.g. 512323123"
            mode="outlined"
            v-model="phone"
            :error="isError2"
            />
            <HelperText v-if="isError2" type="error" visible>
            Phone Number is Required!
          </HelperText>
        </view>
        <view class="item2">
        </view>
        <nb-button class="btn" :on-press="next" info><nb-text class="text">Next</nb-text></nb-button>
    </nb-content>
  </nb-container>
</template>

<style>
.content{
    margin: 28px;
    margin-top: 30px;
}
.label{
    font-weight: bold;
    font-size:20px;
    margin-top:40px;
    margin-bottom: 10px;
}
.btn{
    margin-top: 25px;
    margin-left: 75%;
    border-radius: 10px;
}
.text{
  font-size:20px;
}
</style>

<script>
import { TextInput, HelperText } from 'react-native-paper';

export default {
    data(){
        return{
          email:'',
          phone:'',
          isError1: false,
          isError2: false
        }
    },
    components:{
        TextInput,
        HelperText
    },
    props: {
        navigation: {
            type: Object,
        },
    },
   
    methods:{
        next(){
            const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
            String(this.email.toLowerCase())
            if(this.email.length == 0 || this.email.match(re)){
            this.isError1 = true;
            }
            else{
                this.isError1 = false;
            }
            if(this.phone.length == 0){
                this.isError2 = true;
            }
            else{
                this.isError2 = false;
            }
            if(this.isError1 == false && this.isError2 == false){
                this.navigation.navigate('OtpScreen');
            }
        },
    }
}
</script>