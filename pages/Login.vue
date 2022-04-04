<template>
  <div class="formy">
    <form action="" @submit.prevent="atClick">
      <div class="form">
        <label for="email"  style="background: transparent;" >Email:</label>
        <input type="text" v-model="email">
      </div>
      <div class="form">
        <label for="password" style="background: transparent;">Password:</label>
        <input type="text" v-model="password">
      </div>
          <div class="btn">
          <button>Login</button>
          <!-- <button>Signup</button> -->
          </div>
    </form>
  </div>
</template>

<script>
// import { auth, firebaseAuth} from '@/firebase/index'
export default {
  
  data() {
    return {
      email: '',
      password: '',

    }
  },
  methods: {
    atClick(){
      
      this.$fire.auth.signInWithEmailAndPassword(this.email, this.password)
      .then(() => this.$router.go(-1)) 
      .catch(err => console.log(err)) 
    }
  },

  mounted() {
     this.$fire.auth.onAuthStateChanged((user, err) => {
       if(user){
         this.$router.push('/')
       }
     })
  },
}
</script>
  



<style lang="scss" scoped>
.formy{
  height: 100vh;
  display: grid;
  place-items: center;
  }
  form{
  
    width: 500px;
 
   text-align: center;
  background: rgb(68, 66, 66);
  box-shadow: -5px 10px 25px #000;
  }
  .form{

    place-items: center;
    color: gray;
    
    input {
      border-bottom: solid 2px #02c9b8;
      width: 80wh;
      height: 2em;
      margin-top: 20px ;
      margin-bottom: 20px;
    }
    .btn{
      display: flex;
      justify-content: space-between;
      
     
    }
   
  }
    button{
       
        background: #02c9b8 ;
        margin-bottom: 40px;
        margin-top: 40px;
        padding: 10px 10px;
        margin-top: 20px;
        border-radius: 10px;
        color: #fff;
        width: 120px;
        margin-left: 20px;
      }
</style>