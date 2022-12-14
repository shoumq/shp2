<template>>
  <UserCard :email="emailApi" :phone="phoneApi" :FIO="FIOApi" :adress="adressApi" :imgUrl="imgUrlApi" :nick="nickApi"/>
</template>

<script>
import UserCard from './components/UserCard.vue'
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      emailApi: '',
      phoneApi: '',
      FIOApi: '',
      nickApi: '',
      adressApi: '',
      imgUrlApi: '',
    }
  },
  components: {
    UserCard
  },
  methods: {
    getUserData() {
      axios.get('https://randomuser.me/api/').then((response) => {
        console.log(response.data.results[0])
        this.emailApi = response.data.results[0].email
        this.phoneApi = response.data.results[0].phone
        this.FIOApi = response.data.results[0].name.first + ' ' + response.data.results[0].name.last + ' ' + response.data.results[0].name.title;
        this.adressApi = response.data.results[0].location.city + ', ' + response.data.results[0].location.state
        this.imgUrlApi = response.data.results[0].picture.large,
        this.nick = response.data.results[0].id.name
      })
    }
  },
  mounted() {
    this.getUserData();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
