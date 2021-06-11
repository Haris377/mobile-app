<template>
  <nb-container>
    <nb-content class="content">
        <text class="title">Confirmation Code</text>
         <TextInput
            class="name" 
            label="e.g. 512323-1235675785-8"
            mode="outlined"
            />
      <view class="btn">
      <nb-button transparent light>
        <nb-text class="skip-btn">Skip</nb-text>
      </nb-button>
        <nb-button :on-press="next" class="btn-next" primary><nb-text class="text">Next</nb-text></nb-button>
        </view>
    </nb-content>
  </nb-container>
</template>

<style>
.content{
  margin: 25px;
  margin-top: 55px;
}
.skip-btn{
  color: blue;
  font-size: 20px;
}
.title{
  font-weight:bold;
  font-size: 25px;
  margin-bottom: 20px;
}
.btn{
  flex-direction: row;
  justify-content: space-between;
  margin-top: 20px;
}
.btn-next{
  border-radius: 10px;
}
.text{
  font-size:20px;
}
.option{
  color: rgb(220, 215, 215);
}
</style>

<script>
import { TextInput } from 'react-native-paper';

export default {
  components:{
    TextInput
  },
    data(){
        return{
          
        }
    },
    props: {
        navigation: {
            type: Object,
        },
    },
   
    methods:{
      next(){
        this.navigation.navigate('Password');
      }
    }
}
</script>