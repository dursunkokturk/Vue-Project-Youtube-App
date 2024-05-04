<template>
    <form class="searchForm" @submit.prevent="handleSubmit">

        <!--Input Elementi Icine Girilen Data yi Almak Ve 
            Arama Islemi Yapmak Icin
            v-model Attribute unu Kullanarak 
            data Method Ile Baglanti Kuruyoruz-->
        <input class="searchInput" v-model="searchTerm" type="text">
        <button class="searchBtn">Ara</button>
    </form>
</template>

<script>
    export default {
        emits:['termChange'],
        data() {
            return {
                searchTerm:''
            }
        },
        methods: {
            handleSubmit(){

                // Input Elementine Girilen Data yi searchTerm Ile Aliyoruz
                // Kullanacagimiz Yere termChange Ile Emit Ediyoruz (Gonderiyoruz)
                this.$emit('termChange',this.searchTerm);
                this.searchTerm=''
            }
        },
    }
</script>

<style scoped>
    .searchForm{
        display: flex;
        margin: 20px 0px;
    }
    .searchInput{
        width: 85%;
        padding: 8px;
        margin-right: 20px;
        border-radius: 20px;
    }
    .searchBtn{
        width: 15%;
        border: none;
        background: green;
        color: white;
        font-size: 18px;
        border-radius: 20px;
        cursor: pointer;
    }
</style>