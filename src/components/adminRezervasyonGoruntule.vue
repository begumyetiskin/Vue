<template>

  <div class="adminRezervasyonGoruntule">    
    <div class="header">      
        <label><strong>{{title}}</strong></label>  
        &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        &ensp;&ensp;&ensp;&ensp;&ensp;
      <button class="button" @click="cikisYap">Çıkış Yap</button>         
    </div>

  <div class="menu">
    <ul>      
      <li @click="gitAdminArabaGoruntule"><a href="#adminArabaGoruntule">Arabalar</a></li>
      <li @click="gitAdminMusteriGoruntule"><a href="#adminMusteriGoruntule">Müşteriler</a></li>
      <li @click="gitAdminRezervasyonGoruntule"><a href="#adminRezervasyonGoruntule">Rezervasyonlar</a></li>
    </ul>
  </div>

    <div class="col-md-6">            
            <table border="1">
              <body>
                <tr>
                  <td>Ad Soyad</td>
                  <td>Telefon</td>
                  <td>Araba Model</td>
                  <td>Alış Tarihi</td>
                  <td>Teslim Tarihi</td>
                </tr>
                <tr v-for="(rezervasyon, index) in rezervasyonlar" :key="index">
                <td >                  
                     {{rezervasyon.kullaniciAdSoyad}}                      
                </td>
                <td>
                  {{rezervasyon.kullaniciTel}}
                </td>
                <td>
                  {{rezervasyon.arabaModel}}
                </td>
                <td>
                  {{rezervasyon.alisTarihi}}
                </td>
                <td>
                  {{rezervasyon.teslimTarihi}}
                </td>
                </tr>
              </body>
              
            </table>
            
      </div>
  </div>
</template>

<script>
import httpClient from "../http-common";
export default {
  name: 'adminRezervasyonGoruntule',
  data: function(){
    return{
      title: "Sivas Araç Kiralama",
      rezervasyonlar: []
    }    
  },
  methods: {
      cikisYap() {
          this.$router.push('/ilkEkran');
      },
        getirRezervasyonlar() {
        httpClient
          .get("/rezervasyonlar")
          .then(response => {
            this.rezervasyonlar = response.data; // JSON are parsed automatically.
            console.log(response.data);
          })
          .catch(e => {
            console.log(e);
          });
      },
      refreshList() {
        this.getirRezervasyonlar();
      },
          
      gitAdminArabaGoruntule (){
          this.$router.push('/adminArabaGoruntule');
      },
      gitAdminMusteriGoruntule(){
          this.$router.push('/adminMusteriGoruntule');
      },      
      gitAdminRezervasyonGoruntule (){
          this.$router.push('/adminRezervasyonGoruntule');
      }
  },
  mounted() {
    this.getirMusteriler();
    
  }
}
</script>

<style>

.header{
  padding: 10px;
  margin-top: 0px;
  background-color:#34495e;/*rosybrown;/*;#805664;*/
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  font-size: 20px;
  color:white/*#34495e,seashell*/;
}

.button {
  font-size: 16px;
  border-radius: 4px;
  background-color: white;
  color: black;
  border: 2px solid silver;
  }
  
.button:hover {
  background-color: silver;
  color: white;
}

.rezervasyon{
  padding: 20px;
  margin-top: 75px;
  width: 30%;
  background-color:silver;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  font-size: 20px;
}

body{
  background-image: url("arkaplan1.jpg");  
  margin:0 0;
}

ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    overflow:hidden;
    background-color:#8d8d8b /* #533740 */;
  }

li {
    display:inline-block;
}

li a {
    display: block;
    color: white;
    font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
    font-size: 20px;
    text-align: center;
    padding: 14px 18px;
    text-decoration: none;
}

li a:hover{
    background-color:#34495e; /* burlywood */
}

</style>