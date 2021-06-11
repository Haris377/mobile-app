<template>
  <view class="container">
    <image class="logo" :source="require('../assets/unilever.png')" />
    <!-- <text class="loginText">Login</text> -->
    <view class="input">
      <TextInput
        class="emailInput"
        label="Email"
        mode="outlined"
        outlineColor="blue"
        underlineColor="blue"
      />
    </view>
    <view class="input">
      <TextInput
        class="emailInput"
        label="Password"
        mode="outlined"
        outlineColor="blue"
        underlineColor="blue"
      />
    </view>
    <view class="forgot">
      <view :style="{flexDirection: 'row'}">
        <nb-checkbox
          :style="{marginLeft: 15}"
          :on-press="checked"
          :checked="boolean"
        />
        <text :style="{marginLeft: 15}">Keep me logged in</text>
      </view>

      <text :style="{color: 'blue', marginRight: 20, fontSize: 14}"
        >Forgot Password?</text
      >
    </view>

    <touchable-opacity class="loginBtn">
      <nb-button iconLeft full :on-press="changeRoute">
        <nb-text :style="{color: 'white'}">Login</nb-text>
      </nb-button>
    </touchable-opacity>
    <view class="divider">
      <view :style="{flex: 1, height: 1, backgroundColor: 'gray'}"></view>
      <text :style="{width: 50, textAlign: 'center'}">OR</text>
      <view :style="{flex: 1, height: 1, backgroundColor: 'gray'}"></view>
    </view>
    <touchable-opacity class="gmailLogin">
      <nb-button
        iconLeft
        full
        :on-press="login"
        :style="{backgroundColor: 'rgb(224,99,84)'}"
      >
        <nb-icon :style="{color: 'white'}" active name="logo-google" />
        <nb-text :style="{color: 'white'}">Login with Gmail</nb-text>
      </nb-button>
    </touchable-opacity>
    <touchable-opacity class="gmailLogin">
      <nb-button
        iconLeft
        full
        :on-press="loginFacebook"
        :style="{backgroundColor: 'rgb(26,119,242)'}"
      >
        <nb-icon :style="{color: 'white'}" active name="logo-facebook" />
        <nb-text :style="{color: 'white'}">Login with Facebook</nb-text>
      </nb-button>
    </touchable-opacity>
        <nb-button :on-press="signup" transparent light>
        <nb-text :style="{color: 'blue', marginTop: 20, fontSize: 14}" class="btn-create-account">Create Account</nb-text>
      </nb-button>
    <!-- <text :style="{color: 'blue', marginTop: 20, fontSize: 16}"
      >Create Account</text
    > -->
  </view>
</template>

<script>
import {
  GoogleSignin,
  GoogleSigninButton,
  statusCodes,
} from '@react-native-google-signin/google-signin';
import {
  LoginButton,
  AccessToken,
  LoginManager,
  GraphRequest,
  GraphRequestManager,
} from 'react-native-fbsdk';
import axios from 'axios';
import {Alert} from 'react-native';
import Vue from 'vue-native-core';
import {VueNativeBase} from 'native-base';
Vue.use(VueNativeBase);
import {TextInput} from 'react-native-paper';
import {StatusBar} from 'react-native';

export default {
  // Declare `navigation` as a prop
  props: {
    navigation: {
      type: Object,
    },
  },
  components: {
    TextInput,
  },
  data() {
    return {
      currentUser: '',
      token: '',
      boolean: false,
    };
  },
  methods: {
    signup(){
      this.navigation.navigate('Signup');
    },
    checked() {
      if (this.boolean == true) {
        this.boolean = false;
      } else {
        this.boolean = true;
      }
    },
    changeRoute() {
      this.navigation.navigate('Dashboard');
    },
    async login() {
      GoogleSignin.configure({
        androidClientId:
          '111799500984-jeegtknjrn8jh0jf234mpka342faopp5.apps.googleusercontent.com',
      });
      try {
        await GoogleSignin.hasPlayServices();
        const userInfo = await GoogleSignin.signIn();
        console.log('user' + userInfo);
        this.changeRoute();
      } catch (error) {
        console.log(error);
        if (error.code === statusCodes.SIGN_IN_CANCELLED) {
          // user cancelled the login flow
        } else if (error.code === statusCodes.IN_PROGRESS) {
          // operation (e.g. sign in) is in progress already
        } else if (error.code === statusCodes.PLAY_SERVICES_NOT_AVAILABLE) {
          // play services not available or outdated
        } else {
          // some other error happened
        }
      }
    },
    loginFacebook() {
      LoginManager.logInWithPermissions(['public_profile', 'email']).then(
        function (result) {
          if (result.isCancelled) {
            console.log('Login cancelled');
          } else {
            console.log(
              'Login success with permissions: ' +
                result.grantedPermissions.toString(),
            );
            const data = AccessToken.getCurrentAccessToken().toString();
            console.log('data: ', data);
            this.changeRoute();
          }
        }.bind(this),
        function (error) {
          console.log('Login fail with error: ' + error);
        },
      );
    },
  },
  mounted() {
    console.log('mount');
    StatusBar.setBarStyle('light-content', true);
    StatusBar.setBackgroundColor('#0996AE');
  },
};
</script>

<style>
.container {
  background-color: rgb(255, 255, 255);
  align-items: center;
  margin-top: 40;
  height: 100%;
  width: 100%;
}
.text-color-primary {
  color: blue;
}
.input {
  align-items: center;
  width: 100%;
  margin-top: 20;
}
.inputText {
  margin: 10;
  align-items: flex-start;
}
.loginBtn {
  margin-top: 30;
  width: 90%;
  border-radius: 10;
  overflow: hidden;
}
.gmailLogin {
  width: 90%;
  margin-top: 20;
  color: white;
  border-radius: 10;
  overflow: hidden;
}
.logo {
  height: 100;
  width: 90;
}
.loginText {
  margin-top: 20;
  font-size: 20;
}
.emailInput {
  width: 90%;
}
.float {
  width: 90%;
}
.pwdInput {
  width: 90%;
}
.divider {
  margin-top: 10;
  flex-direction: row;
  align-items: center;
}
.forgot {
  width: 100%;
  justify-content: space-between;
  margin-top: 30;
  flex-direction: row;
}
.btn-create-account{
  margin-left: 130;
}
</style>
