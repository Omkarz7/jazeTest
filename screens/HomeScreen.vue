<template>
  <view class="container">
            
    <text>This is the Home screen</text>
    <view class="top-right"><button title="Logout" color="red" @press="logout"></button></view>
    <view class="custom-button"><button title="Click verify token" @press="verifyToken" ></button></view>
  </view>
</template>

<script>

import axios from "axios";
import { AsyncStorage } from 'react-native'
export default {
  props: {
    navigation: { type: Object }
  },
  data(){
    return{
        server:axios.create({
        baseURL: "http://192.168.43.250:3600",
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json"
       },
       timeout: 10000
      }),
      sortByStartDate:true
    }
  },
  created(){
    this.server.interceptors.request.use(
    async function(config){
      config.headers.Authorization = await AsyncStorage.getItem('authToken');
      return config;
  },
  error => alert(error)
);
  },
  methods: {
  async verifyToken() {
      try{
        await this.server.get("/r/getMasterplan?sortByStartDate=" + this.sortByStartDate)
        alert('Token verifed')
      }catch(error){
        alert(error)
      };
    },
    async logout(){
      await AsyncStorage.removeItem('authToken');
      this.navigation.navigate('Login');
    }
  }
}
</script>

<style>
.container {
  align-items: center;
  justify-content: center;
  flex: 1;
}

.custom-button{
  margin: 15%;
  height: 5%; 
  width: 45%; 
}

.top-right {
  position: absolute;
  top: 8px;
  right: 16px;
  font-size: 18px;
}
</style>
