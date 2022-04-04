<template>
        <div style="color:aliceblue;">
            <div v-if="musics != null" >
            
            <div >
                <div>
                    <img :src="musics.images[0].url" alt=""   />
                </div>
                {{ musics.name }}
                <!-- <p>{{ musics.release_date }}</p> -->
                  <p>
                   Released: {{
                new Date(musics.release_date).toLocaleString('en-us', {
                  month: 'long',
                  day: 'numeric',
                  year: 'numeric',
                })
              }}
               
                </p>

                
               <div  class="cover">
                     <ol v-for="(items, index ) in musics.tracks.items" :key="index">

                <li>Track Title: {{items.name}}</li>
                <li>Track Number: {{items.track_number}}</li>
                <li>Duration: {{items.duration_ms}}</li>
                </ol>
               </div>
            </div>
        
        </div>
        </div>
   
</template>

<script>
export default {

    data() {
        return {
            musics: null
        }
    },
    mounted(){

        const musicid = JSON.parse(localStorage.getItem(`albumid:${this.$route.params.musicid}`))

        if(!musicid){

            fetch('https://api.spotify.com/v1/albums/' + this.$route.params.musicid, 
                {
                    headers: {
                        'Authorization': 'Bearer ' + 'BQAgvuW9puxZXv43QGXCmwab-BOMO4GSc1AfyJvnHSJp7zX1m07Q3yU9Q1J43611t7i5iGzvLqzS5DcUik0'

                    },
                }
            )
            .then((res) => res.json())
        .then(data => {
            this.musics = data
            localStorage.setItem(`albumid:${this.$route.params.musicid}`, JSON.stringify(this.musics))
            console.log(this.musics);
            })
            .catch((err) => console.log(err))
        }else{
            this.musics = musicid
            // console.log(musicid);
        }
        
    }
    
}
</script>


<style lang="scss">
img{
    width:400px;
    height: 400px;
}
ol{
    margin-block: 20px;
     padding-left:20px;
}
.cover{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
}
</style>