<template>
    <ul class="videoList">

        <!--SearchBar.vue Dosyainda videos Degiskeni Uzerinden Gelen Data lari
            VideoListItem.vue Dosyasinda Listeliyoruz,
            Ancak Ekranda Gosterme Islemini
            VideoList.vue Dosyasi Uzerinden Yapiyoruz-->
        <!--v-for Kisminda 
            Array Icindeki Degerleri Tarama Isleminden Sonra 
            Her Birini Verilen Isim Ile Geziyoruz-->
        <!--key Kisminda v-for Kisminda Gezme Islemi Bittiginde 
            Her Element Icin Gereken key Degerini Veriyoruz-->
        <!--video Kisminda 
            key Degerleri Ile Birlikte Video Elementlerini Yazdiriyoruz-->
        <!--videoSelect Kisminda Arama Isleminden Sonra 
            Gelen Video Listesi Icinden 
            Tiklanilan Videonun Acilmasini Saglar-->
        <VideoListItem @videoSelect="onVideoSelect" v-for="video in videos" :key="video.etag" :video="video"/>        
    </ul>
</template>

<script>

    // Array Icindeki Videolarin Listesini Aliyoruz
    import VideoListItem from './VideoListItem.vue'
    export default {

        // App.vue Dosyasindaki videos Icinde Bulunan Data lari
        // props Olarak Aliyoruz
        props:['videos'],
        emits:['videoSelect'],
        components:{

            // Array Icindeki Videolarin Listesini 
            // Component Uzerinden Gosterilmesini Sagliyoruz
            VideoListItem
        },
        methods: {
            onVideoSelect(video){

                // Uzerine Tiklanilan Videonun Acilmasi Icin 
                // Bilgilerini Gonderiyoruz
                this.$emit('videoSelect',video)
            }
        },
    }
</script>

<style scoped>
    .videoList{
        list-style-type: none;
        width: 100%;
    }
</style>