<template>
  <app-navigator></app-navigator>
</template>

<script>
import {createAppContainer, createStackNavigator} from 'vue-native-router';
import Signup from "./screens/Signup.vue";
import OtpConfirmation from "./screens/OtpConfirmation.vue";
import LoginScreen from './screens/Login.vue';
import DashboardScreen from './screens/Dashboard.vue';
import OnboardingScreen from './screens/Onboarding.vue';
import AccountInfo from "./screens/AccountInfo";
import Password from "./screens/Password.vue";
import Vue from "vue-native-core";
import { VueNativeBase } from "native-base";
Vue.use(VueNativeBase);

const StackNavigator = createStackNavigator(
  {
   Signup: {
      screen: Signup,
      navigationOptions: ({navigation}) => ({title: "Create Account"})
    },
    AccountInfo: AccountInfo,
    Password: Password,
    OtpScreen: OtpConfirmation,
    Login: {
      screen: LoginScreen,
      navigationOptions: {
        headerTitle: 'Login',
        marginTop: 20,
      },
    },
    Dashboard: {
      screen: DashboardScreen,
    },
    Onboarding: {
      screen: OnboardingScreen,
      navigationOptions: {
        headerTransparent: true,
      },
    },
  },
  {
    initialRouteName: 'Onboarding',
	 defaultNavigationOptions: {
      title: 'Create Account',
      headerStyle: {
         backgroundColor: "#ffffff",
      },
      headerTintColor: "#4D6FCF",
      //header: null,
      headerTitleStyle: {
        fontWeight: "bold",
        color:"#000000",
        marginLeft:68,
      }
    },
  },
);
const AppNavigator = createAppContainer(StackNavigator);
export default {
  components: {AppNavigator},
};
</script>
