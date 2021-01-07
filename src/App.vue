<template>
  <div id="app"  >
   
   <main>
     <div class="search-box">
        <input type="text"  class="search-bar" 
        placeholder="Search"
        v-model="query"
        @keypress="fetchWeather"
        />
        
     </div>
     <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
       <div class="location-box">
         <div class="location" v-if="weather.name">{{weather.name}}, {{weather.sys.country}}</div>
                  <div class="location" v-else>{{dateBuilder()}}</div>

         
         <div class="date">{{dateBuilder()}}</div>


         <div class="weather-box">
           <div class="temp">{{ Math.round(weather.main.temp) }} </div>
           <div class="weather">{{weather.weather[0].main}}</div>
         </div>
       </div>
     </div>
   </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return { api_key:'6d8d5f1021fd5bb8bdea1d220d7ce35e',
              url_base:'https://api.openweathermap.org/data/2.5/',
              query:'',
              weather:{}

              
    }
    },
    methods:{
      fetchWeather(e){
        if(e.key=="Enter"){
          fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res=>{
              return res.json();
          }).then(this.setResults);
        }

      },
      setResults(results){
        this.weather=results;

      },
      dateBuilder(){
        let d = new Date();
        let months= ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
        let days = ['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
        
        let day = days[d.getDay()];
        let date = d.getDate();
        let month = months[d.getMonth()];
        let year = d.getFullYear();

        return `${day} ${date} ${month} ${year}`;

      }

    }
  

  
}
</script>

<style>
*{
  margin:0;
  padding: 0;
  box-sizing: border-box;
  font-size:18px;
}

body{
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
 background: rgba(202, 245, 166, 0.24);
  justify-content:center;
}
body.warm{
   width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
 background: rgba(218, 113, 87, 0.808);
  justify-content:center;

}

#app{
  background: rgba(243, 236, 236, 0.35);
box-shadow: 0 8px 32px 0 rgba( 31, 38, 135, 0.37 );
backdrop-filter: blur( 4.0px );
-webkit-backdrop-filter: blur( 4.0px );
border-radius: 10px;
  display: flex;
  align-items: start;
  justify-content: center;
  width: 450px;
  height: 450px;
  
}


.search-box .search-bar{
  margin-top: 45px;
  position: relative;
  display:flex;
  align-content: flex-start;
  width:350px;
  height: 35px;
  outline: none;
  border: none;
  background: rgba(206, 249, 255, 0.418);

  border-radius: 16px 0px 16px 0px;
  box-shadow:  0px 0px 8px rgba(162, 215, 250, 0.356);
  transition: 0.4s;

}
.search-box .search-bar:focus{
    box-shadow:  0px 0px 24px rgba(162, 215, 250, 0.45);
      border-radius: 0px 16px 0px 16px;

}
.search-box .search-bar::placeholder{
    color:rgba(46, 38, 38, 0.527);
    font-size: .8rem;
    padding-left:10px ;


}

.location-box .location{
  color: rgb(167, 158, 158);
  font-size: 2rem;
  font-weight: 600;
  text-align: center;
  margin-top: 85px;

}
.location-box .date{
  color: rgb(167, 158, 158);
  font-size: 1.2rem;
  margin-top:15px ;
  font-weight: 400;
  font-style: italic;
  text-align: center;
}

.weather-box{
  text-align: center;

}

.weather-box .temp {
  font-size: 1.5rem;
  padding:10px 25px 25px;
  color: rgb(189, 159, 159);
  font-weight: 800;
  

}
.weather-box .weather {
  font-size: 2rem;
  padding:10px 25px 25px;
  color: rgb(151, 125, 125);
  font-weight: 600;
  

}

</style>
