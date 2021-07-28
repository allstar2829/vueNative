<template>
  <app-navigator></app-navigator>
</template>

<script>
import {createStackNavigator} from "react-navigation-stack";
import {createAppContainer} from "react-navigation";

import Home from "./screens/Home.vue"; 
import DetailsScreen from "./screens/DetailsScreen.vue";

const StackNavigator = createStackNavigator(
  {
    Home: Home,
    Details: DetailsScreen,
  },
  {
    initialRouteName: 'Home',
  }
);

const AppNavigator = createAppContainer(StackNavigator);
export default {
  components: { AppNavigator },
}
</script>