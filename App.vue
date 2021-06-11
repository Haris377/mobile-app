<template>
  <app-navigator></app-navigator>
</template>

<script>
import {createAppContainer, createStackNavigator} from 'vue-native-router';
import LoginScreen from './screens/Login.vue';
import DashboardScreen from './screens/Dashboard.vue';
import OnboardingScreen from './screens/Onboarding.vue';

const StackNavigator = createStackNavigator(
  {
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
  },
);
const AppNavigator = createAppContainer(StackNavigator);
export default {
  components: {AppNavigator},
};
</script>
