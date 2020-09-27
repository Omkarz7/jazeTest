<template>
<view class="container">

<text>  Sign In </text>

    <text-input class="input" v-model="username" placeholder="Username"/>
    <text-input class="input" v-model="password" secure-text-entry style={styles.default} placeholder="Password" />
    <button
        @press="goToHomeScreen"
        title="Login"
        class="custom-button"
    />
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
      username:'',
      password:'',
      server:axios.create({
        baseURL: "http://192.168.43.250:3600",
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json"
       },
       timeout: 10000
      })
    }
  },
  methods: {
    async goToHomeScreen() {
      //simple validation for now. Using vuelidate seems excessive
      if(this.username==='' || this.password===''){
        alert('Please enter your credentials')
        return
      }
      let userCredentials = {Username:this.username,Password:this.password}
      try{
        let response = await this.server.post("/o/login", userCredentials)


        await AsyncStorage.setItem('authToken', response.headers.authorization);
        this.navigation.navigate("Home");
      }catch(error){
            alert(error)
        }
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

.input{
  height: 5%; 
  width: 75%; 
  borderColor: gray; 
  borderWidth: 1;
  margin: 2%;
  border-radius: 7px;/*gives error if I use % instead of px*/
  }

.custom-button{
  height: 5%; 
  width: 15%; 
    margin: 2%;
  border-radius: 7px;/*gives error if I use % instead of px*/
}
</style>