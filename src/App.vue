<template>
    <div class="container">
        <h1 class="title">Youtube Uygulaması</h1>

        <!--SearchBar.vue Dosyasinda termChange Ile Emit Edilen Data yi Yazdiriyoruz-->
        <SearchBar @termChange="onTermChange"/>
        <div class="detailDiv">

          <!--Uzerine Tiklanilan Videonun Gosterilmesini Sagliyoruz-->
          <VideoDetail :video="selectedVideo"/>

          <!--VideoList.vue Dosyasinda Listelenen Sonuclari
                Component Uzerinden Listeleme Islemi Yapiyoruz-->
            <!--videoSelect Kisminda 
                Uzerine Tiklanilan Videonun 
                Ekranda Gosterilmesini Sagliyoruz-->
          <VideoList @videoSelect="onVideoSelect" :videos="videos"/>
        </div>
    </div>
</template>

<script>
    import SearchBar from './components/SearchBar.vue'
    import VideoList from './components/VideoList.vue'
    import VideoDetail from './components/VideoDetail.vue'
    import Axios from 'axios'

    export default {
        name: 'App',
        components: {
            SearchBar,
            VideoList,
            VideoDetail
        },
        data() {
            return {

                // then Blok Icinde 
                // videos Degiskenine Alinan Cevaplari
                // Array Icinde Topluyoruz
                videos:[],

                // Ilk Olarak Secilmis Bir Video Olmadigi Icin
                // Degerini null Yapiyoruz
                // Video Secilme Islemi Yapilirsa Deger Degisecek
                selectedVideo:null
            }
        },
        methods: {
            onVideoSelect(video){
                this.selectedVideo=video
            },

            // Input Icine Girilen Data yi Aliyoruz
            // onTermChange Metodu Icinde searchTerm Parametresi Uzerinden Gelen Data yi 
            // console da Yazdiriyoruz
            onTermChange(searchTerm)
            {   

                // Youtube Baglantisi Icin Api Istegi Atiyoruz 
                Axios.get('https://www.googleapis.com/youtube/v3/search',{
                    params:{
                        part:'snippet',

                        // Arama Isleminin Sonucunda Elde Edilecek Veri Turu
                        type:'video',

                        // Arama Isleminin Sonucunda Elde Edilecek Verinin Sahip Oldugu key
                        key:'AIzaSyDwNXwydLUybGBicl7GdDPlJuzvPeV1bYM',

                        // Input Elementi Icine Girilen Data yi
                        // q Degiskeni Icine Aliyoruz
                        q:searchTerm
                    }
                }).
                then(response => {           
                    console.log(response);

                    // Api Uzerinden Yapilan Baglanti Isteginden Gelen Cevabi
                    // videos Degiskenine Atama Yapiyoruz
                    this.videos = response.data.items
                  }
                )
                .catch(error=> {          
                    console.log(error);
                  }
                )        
            }
        },
    }
</script>

<style>
    *{
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    .container{
        max-width: 1200px;
        width: 100%;
        margin: 50px auto; 
    }
    .title{
      text-align: center;
    }
    .detailDiv{
      display: flex;
    }
</style>