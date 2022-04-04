<template>
    <div class="all home">
     <h2 v-if="iranu != ''">Welcome {{iranu}}</h2>

                  <!-- Search -->
    
    <div class="container search" >
        <input 
     type="text"
     placeholder="Search"
     >
      <button  class="button"  >
        Clear Search
      </button>
    </div>

             <div class="container movies">
             
                        <div v-if="musics.length" id="movie-grid" class="movies-grid">
                    <div v-for="(music, index) in musics" :key="index" class="movie">
            <div class="movie-img">
                <img :src="music.images[0].url" alt="">
            
                <div class="overview">
                        <p> 
                  Name: {{music.artists[0].name}}
                   </p>
                  <p>
                  Album: {{music.name}}
               
                </p>
                
                </div>
                
                   
                  
              </div>

                <div class="release">
                 
                <p>
                   Released: {{
                new Date(music.release_date).toLocaleString('en-us', {
                  month: 'long',
                  day: 'numeric',
                  year: 'numeric',
                })
              }}
               
                </p>
                <p>
                  Tracks: {{music.total_tracks}}
               
                </p>
                </div>
               <NuxtLink class="button button-light" :to="'/musics/' + music.id">Get More Info</NuxtLink>

               <!-- <a :href="music.href" target="_blank" class="button button-light">Get More Info</a> -->
        </div>
                </div>
             </div>


             </div>




   
</template>

<script>
import axios from 'axios'
export default {
        data()  {
            return {
                musics: [],
                iranu: '',
                clientID: '4429c7adb6684f358fbf40a4bd550d82',
                clientSecret: '7257468d64e64eb69b65242f7ff521ad'
            }
        },
    
      mounted() {
      this.$fire.auth.onAuthStateChanged((user, err) => {
         if (!user) {
            this.$router.push('/login')
         } else {
            this.iranu = this.$fire.auth.currentUser.displayName
         }
      })
     
//   AQCZkFMHDo0M5rEDBJlhgiD8cnYB0gj12EiUuKBulmIc-4jiGux354toLT9x_AcGxsrNfYWIQJFUlfLFmBOeAqrEXeOlnwJGB2OaeV1f3Q6iY3WB1LKcZVeMWQt3mKnNdHZYmSC0ZZ28tm6frfwYTkllIN1kTZZHV9ahPQkJdVVLTmP7HapxUKiEASfAWeGMquU

            const shakur = JSON.parse(localStorage.getItem('albums'))

        if(!shakur){
            fetch('https://api.spotify.com/v1/search?type=album&q=album', 
                {
                    headers: {
                        'Authorization': 'Bearer ' + 'BQB-NUtK7adeGjJ4nPKdX9q7kwVghJpFXZxtGKLOg33WorrINik_HXvzBTmuCEr8JF7qpEhKUa92kuN3-rQ'

                    },
                }
            )
            .then((res) => res.json())
        .then(data => {
            this.musics = data.albums.items
            localStorage.setItem('albums', JSON.stringify(this.musics))
            console.log(this.musics);
            })
            .catch((err) => console.log(err))
        }else {
            this.musics = shakur
        }


    //   console.log(this.musics);
    }

 
}
</script>

<style lang="scss" scoped>

p{
    background: transparent;
    text-transform: capitalize;
}
.all{
    color: #fff;
    }
    h2{
        color: #fff;
    }

    h2{
  color: white;
}
.home {
  .loading {
    padding-top: 120px;
    align-items: flex-start;
  }
  .search {
    display: flex;
    padding: 32px 16px;
    input {
      max-width: 350px;
      color: #fff;
      width: 100%;
      padding: 12px 6px;
      font-size: 14px;
      border: solid 1px #02c9b8;
      &:focus {
        outline: none;
        border: solid 1px #fff;
      }
    }
    .button {
      border-radius: 10px;
      border-bottom-left-radius: 0;
      border: solid 1px #fff;
      color: #02c9b8;
      margin-left: 20px;
      padding: 10px;
      

    }
  }
  .movies {
    padding: 32px 16px;
    .movies-grid {
      display: grid;
      column-gap: 32px;
      row-gap: 64px;
      grid-template-columns: 1fr;
      @media (min-width: 500px) {
        grid-template-columns: repeat(2, 1fr);
      }
      @media (min-width: 750px) {
        grid-template-columns: repeat(3, 1fr);
      }
      @media (min-width: 1100px) {
        grid-template-columns: repeat(4, 1fr);
      }
      .movie {
        position: relative;
        display: flex;
        flex-direction: column;
        .movie-img {
          position: relative;
          overflow: hidden;
          &:hover {
            .overview {
              transform: translateY(0);
            }
          }
          img {
            display: block;
            width: 100%;
            height: 100%;
          }
          .review {
            position: absolute;
            top: 0;
            left: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            width: 40px;
            height: 40px;
            background-color: #02c9b8;
            color: rgb(255, 255, 255);
            border-radius: 0 0 16px 0;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
              0 2px 4px -1px rgba(0, 0, 0, 0.06);
          }
          .overview {
            line-height: 1.5;
            position: absolute;
            bottom: 0;
            border-radius: 10px 10px 10px 0;
            background-color: #02c9b8;
            padding: 12px;
            color: rgb(2, 32, 32);
            transform: translateY(100%);
            transition: 0.3s ease-in-out all;
            
          }
        }
        .info {
          margin-top: auto;
          .title {
            margin-top: 8px;
            color: #fff;
            font-size: 20px;
          }
          .release {
            margin-top: 8px;
            color: #c9c9c9;
          }
          .button {
            margin-top: 8px;
            background: #02c9b8;
            height:3em;
            width: 4em;

          }
        }
      }
    }
  }
}
</style>