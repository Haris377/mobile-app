<template>
  <nb-container>
    <nb-content class="content">
      <view class="pass">
        <text class="title">Password</text>
        <TextInput
            class="name" 
            label="e.g. 512323123"
            mode="outlined"
            v-model="password"
            :onChangeText= "onClick"
            />
      </view>
      <view class="check-items">
      <nb-list-item>
        <nb-checkbox :checked="checked1" color="blue"/>
        <nb-body>
          <nb-text>Contains atleast one lowercase letter</nb-text>
        </nb-body>
      </nb-list-item>
      <nb-list-item>
        <nb-checkbox :checked="checked2" color="blue"/>
        <nb-body>
          <nb-text>Contains atleast one Uppercase letter</nb-text>
        </nb-body>
      </nb-list-item>
      <nb-list-item>
        <nb-checkbox :checked="checked3" color="blue"/>
        <nb-body>
          <nb-text>Contains atleast one number</nb-text>
        </nb-body>
      </nb-list-item>
      <nb-list-item >
        <nb-checkbox :checked="checked4" color="blue"/>
        <nb-body>
          <nb-text>Contains atleast one special character</nb-text>
        </nb-body>
      </nb-list-item>
      <nb-list-item>
        <nb-checkbox :checked="checked5" color="blue"/>
        <nb-body>
          <nb-text>Contains atleast 8 character long</nb-text>
        </nb-body>
      </nb-list-item>
      </view>
      <nb-button :on-press="next" class="btn" info><nb-text class="btn-text">Done</nb-text></nb-button>
    </nb-content>
  </nb-container>
</template>

<style>
.content{
  margin: 20px;
}
.pass{
  margin: 12px;
}
.title{
  font-weight: bold;
  font-size: 30px;
  margin-bottom: 15px;
}
.label{
  margin-bottom: 10px;
}
.btn-text{
  font-size: 18px;
  font-weight: bold;
}
.check-items{
  margin-top: 15px;
}
.btn{
  width: 24%;
  height: 60px;
  border-radius: 10;
  margin-left: 75%;
  margin-top: 25px;
}
</style>

<script>
//import axios from "axios";
import { TextInput } from 'react-native-paper';

export default {
    components: {
    TextInput
  },
  data(){
    return{
      checked1: false,
      checked2: false,
      checked3: false,
      checked4: false,
      checked5: false,
      password: ''
    }
  },
 props: {
    navigation: {
      type: Object
    }
  },
  watch:{

  },
  methods: {
    next(){
        if(this.checked1 == true && this.checked2 == true && this.checked3 == true && this.checked4 == true && this.checked5 == true){
          this.navigation.navigate('Login');
        }
    },
    onClick(){
       if(this.password.match(/[a-z]/)){
          this.checked1 = true;
        }
        else{
          this.checked1 = false;
        }
        if(this.password.match(/[A-Z]/)){
          this.checked2 = true;
        }
        else{
          this.checked2 = false;
        }
        if(this.password.match(/[0-9]/)){
          this.checked3 = true;
        }
        else{
          this.checked3 = false;
        }
        if(this.password.match(/[*@!#%&()^~{}]+/)){
          this.checked4 = true
        }
        else{
          this.checked4 = false;
        }
        if(this.password.length >= 8){
           this.checked5 = true
        }
        else{
          this.checked5 = false;
        }
    },
    click(){
      if(this.checked == true){
          this.checked = false
      }else{
        this.checked = true
      }
    },
  },
};
</script>