<template>
    <section class="cl">
         <br><br><br><br><br><br><br><br>
    <article class="clanak">
        <div class="slikaClanka" style="background-image: url('https://www.teklic.hr/slike/2018/10/ki%C5%A1a3.jpg')"> </div>
        <h1> Rijeka je bila najkišovitiji grad na svijetu </h1>
        <p> Sa 249,5 litara kiše po četvornome metru, postaja Rijeka Kozala uvjerljivo “vodi” iza 
            drugoplasiranog Sanhu Daoa u Kini (141 litra) i zračne luke Shreveport u SAD-u (106 litara). </p> <br>
           <button @click="goToRijekaKisa()"> Pročitajte više... </button>
            
    </article>   

        <article class="clanak">
        <div class="slikaClanka" style="background-image: url('http://abcgeografija.com/wp-content/uploads/2021/03/20210323-Svjetski-meteoroloski-dan.jpg')"> </div>
        <h1> Znate li kada je svjetski meteorološki dan? </h1>
        <p> Svjetski meteorološki dan obilježava se svake godine u znak sjećanja na 23. ožujka 1950. godine, 
            kada je u Ženevi službeno osnovana Svjetska meteorološka organizacija (WMO). </p> <br>
            <button @click="goToMeteorologija()"> Pročitajte više... </button>
    </article>

        <article class="clanak">
        <div class="slikaClanka" style="background-image: url('https://img.24sata.hr/QRWbKQ9FTD7xbZgiPMCBmJ5xjho=/1243x700/smart/media/images/2020-35/suvi-horz2.jpg')"> </div>

        <h1> Znate li koje je boje sunce? </h1>
        <p> Sunce, velika zvijezda našeg solarnog sustava, svake sekunde pretvori nevjerojatnih četiri milijuna tona tvari u energiju. 
            No nebeski div koji je omogućio život na Zemlji ima svoj rok trajanja. Znate li koji je? </p> <br>
            <button @click="goToSunce()"> Pročitajte više... </button>
    </article>

    </section>
</template>

<script>
export default {
     methods:{
   goToRijekaKisa(){
   this.$router.push('/rijekaKisa'); 
      }, 
  

   goToMeteorologija(){
   this.$router.push('/meteorologija'); 
      },

   goToSunce(){
   this.$router.push('/sunce'); 
      } 
     }
}
</script>

<style scoped>
.cl {
    display:flex;
    flex-flow: row wrap;
    background-image: url('https://img.24sata.hr/cTPDwobNnY1MHobc22V2iP0samY=/640x360/smart/media/images/2017-43/dreamstime_xl_47506952.jpg');
    background-repeat:repeat;
    background-size: 100%;
}

.clanak {
    box-sizing: border-box;
    width: 100%;
    padding: 20px;
    border: 1px solid #ccc;
    box-shadow: 0 2px 2px #aaa;

}

.slikaClanka {
    background-position: center;
    background-size: cover;
    margin-left:220px;
    width:60%;
    height: 440px;
    border-radius: 40px;
    border-width: 3px;
    display:block;
    margin:auto;
}

h1 {
text-align: center;
margin-top: 20px;
font-size:30px;
font-family: Georgia, 'Times New Roman', Times, serif;

}

p {
    text-align: center;
    margin-top:10px;
    font-size:20px;
    font-family:Arial, Helvetica, sans-serif;
}

button{
    display:block;
    margin:auto;
    font-family: Georgia, 'Times New Roman', Times, serif;
    font-size: 22px;
    color:blue;
    background-color: yellow;
    border-style: double;
    border-radius: 10%;
    filter: drop-shadow(0px 5px 3px black);
}

button:hover{
    font-style: bold;
    font-size:27px;
    filter: drop-shadow(0px 10px 3px black);

}

</style>