<template>
  <app-navigator></app-navigator>
</template>

<script>
import {
  createAppContainer,
  createStackNavigator,
} from "vue-native-router";

import HomeScreen from "../screens/HomeScreen.vue";
import Login from "../screens/Login.vue";

const StackNavigator = createStackNavigator(
  {
    Home: HomeScreen,
    Login: Login,
  },
  {
    initialRouteName: 'Login',
  }
);

const AppNavigator = createAppContainer(StackNavigator);

export default {
  components: { AppNavigator },
}
</script>