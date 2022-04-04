<template>
    <div class="hero">
       <div><nuxt-link to="/" style="color:white; text-decoration: none;">FlexZone</nuxt-link> </div> 
       <div>
            <ul>
                <li> <nuxt-link to="/movies" style="color:white; text-decoration: none;">Movies</nuxt-link> </li>
                <li><nuxt-link to="/music" style="color:white; text-decoration: none;">Musics</nuxt-link> </li>
                <!-- <li><nuxt-link to="/meetup" style="color:white; text-decoration: none;">MeetUp</nuxt-link> </li> -->
                <nuxt-link to="/login" style=" text-decoration: none;" v-if="!validateUser"><button >Login</button></nuxt-link>

                <button @click="logOut" v-else>Logout</button>
                
                <nuxt-link to="/signup" style=" text-decoration: none;"><button >SignUp</button></nuxt-link>
            </ul>
       </div>

       
    </div>
</template>

<script>
export default {
    data() {
        return {
            validateUser: false,
            

        }
    },
    mounted() {
        
            return this.$fire.auth.onAuthStateChanged((user, err) => {
                if(user) {
                    this.validateUser = true
                }else{
                    this.validateUser = false
                }
            })
        
    },

    methods: {
        logOut(){
            this.$fire.auth.signOut()
            // console.log('res');
            
                .then(() =>{
                    this.$router.push('/')
                })
            
        }
    },
}
</script>



<style lang="scss" scoped>
        .hero{
            display: flex;
            justify-content: space-between;
            padding: 0 40px;
            align-items: center;
            color: #fff;
            height: 3em;

            ul{
                display: flex;
                list-style-type: none;

                
            }

            li{
                padding-right: 20px;
                margin-top: 10px;
            }

            li:hover{
             border-bottom: solid 1px blue;
             padding-left: 20px;
            border-top: dotted 1px lightblue;
            }

            button{
                background: #fff;
                color: #212121;
                margin-right: 10px;
                padding: 10px;
                font-size: 12px;
                border-radius: 5px;

               
            }
        }
</style>