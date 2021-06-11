<template>
  <view class="container">
    <image
      :style="{width: 200, height: 200, marginBottom: 20}"
      :source="{
        uri: image,
      }"
    />
    <text :style="{marginBottom: 10}">{{ info.name }} {{ userInfo.name }}</text>
    <text :style="{marginBottom: 10}"
      >{{ info.email }} {{ userInfo.email }}</text
    >
    <!-- <button :on-press="getInfo" title="get info"></button> -->
    <view :style="{marginBottom: 10}"></view>
    <button :on-press="signOut" title="logout"></button>
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
export default {
  props: {
    navigation: {
      type: Object,
    },
  },
  data() {
    return {
      info: [],
      userInfo: [],
      image:
        'https://cdn4.iconfinder.com/data/icons/small-n-flat/24/user-alt-512.png',
      loginWithGmail: false,
    };
  },
  methods: {
    loginScreen() {
      this.navigation.navigate('Login');
    },
    // async getInfo() {
    //   const currentUser = await GoogleSignin.getCurrentUser();
    //   console.log(currentUser.user.email);
    //   this.info = currentUser.user;
    //   console.log(this.info);
    //   if (this.image != '') {
    //     this.image = '';
    //   } else {
    //     this.image = this.info.photo;
    //   }
    // },
    async signOut() {
      if (this.loginWithGmail == true) {
        try {
          console.log('Gmail LOgout');
          await GoogleSignin.revokeAccess();
          await GoogleSignin.signOut();
          this.loginScreen();
          this.user = null; // Remember to remove the user from your app's state as well
        } catch (error) {
          console.error(error);
        }
      } else {
        LoginManager.logOut();
        console.log('Facebook LOgout');
        this.loginScreen();
      }
    },
    async responseCallBack(error, result) {
      if (error) {
        console.log('Error fetching data: ' + error.toString());
        this.loginWithGmail = true;
        const currentUser = await GoogleSignin.getCurrentUser();
        console.log(currentUser.user.email);
        this.info = currentUser.user;
        console.log(this.info);
        this.image = this.info.photo;
        if (this.info.photo == null) {
          this.image =
            'https://cdn4.iconfinder.com/data/icons/small-n-flat/24/user-alt-512.png';
        }
      } else {
        console.log('Success fetching data: ' + result.toString());
        console.log('result:', result);
        this.userInfo = result;
        console.log(
          result.name,
          ' ',
          result.email,
          ' ',
          this.userInfo.picture.data.url,
        );
        this.image =
          'https://graph.facebook.com/' + result.id + '/picture?type=large';
        if (this.userInfo.picture.data.url == null) {
          this.image =
            'https://cdn4.iconfinder.com/data/icons/small-n-flat/24/user-alt-512.png';
        }
      }
    },
  },
  async mounted() {
    const grp = new GraphRequest(
      '/me?fields=name,email,picture.type(large)',
      null,
      this.responseCallBack,
    );

    new GraphRequestManager().addRequest(grp).start();
  },
};
</script>

<style>
.container {
  background-color: white;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-color-primary {
  color: blue;
}
</style>
