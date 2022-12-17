<template>
<UserCard v-bind:userData = "userData" />
</template>

<script>
import UserCard from './components/UserCard.vue'

export default {
  name: 'App',
  components: {
    UserCard
  },
  data: () => ({
    userData:{
    }
  }),
  mounted(){
    this.getList()
  },
  methods:{
    getList(){
      this.axios.get('https://randomuser.me/api/')
      .then((response) => {
        const data = response.data.results[0]
        this.userData = {
          photoUrl: data.picture.thumbnail,
          userNickname: data.name.first,
          userEmail:data.email,
          userFIO: `${data.name.title} ${data.name.first} ${data.name.last}`,
          userPhone: data.phone,
          userAdress:`${data.location.street.name} ${data.location.city} ${data.location.country}`
        }
      })
    }
  } 
}
</script>

<style>

</style>
