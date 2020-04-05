<template>
    <div class="container">
        <div class="box">
            <h1 class="title">Search Your Domain</h1>
            <div class="search">
                <input 
                    type="text" 
                    placeholder="namadomain.com" 
                    v-model="keyword" 
                    class="search__input"
                    :class="{'error':isEmpty}"
                    @input="onInput" 
                    @keyup.enter="onSearch"                    
                />
                <button class="search__button" @click="onSearch">
                    <span class="icon-search"></span>
                    Search
                </button>
            </div>

            <div v-if="results.length > 0" class="result">
                <div class="result__list" v-for="(result,index) in results" :key="index">
                    <p class="result__list__name">Domain is available!</p>
                    <button v-if="!result.status" class="result__list__buy" @click="onClickBuy(result)">Buy</button>
                    <span v-else class="result__list__purchased">Purchased</span>
                </div>
            </div>
                     
        </div>
    </div>
</template>

<script>
export default {
    name: 'Home',
    data(){
        return {
            keyword: '',
            results: [],
            recommendations: [],
            isSubmit: false,
            domainList: [
                {
                    name: 'domainyanglagidicari.space',
                    price: 'Rp 100.000',
                    status: false
                },
                {
                    name: 'domainyanglagidicari.net',
                    price: 'Rp 50.000',
                    status: false
                },
                {
                    name: 'domainyanglagidicari.org',
                    price: 'Rp 70.000',
                    status: false
                },
                {
                    name: 'domainlain.com',
                    price: 'Rp 30.000',
                    status: false
                },
                {
                    name: 'domainlain.net',
                    price: 'Rp 10.000',
                    status: false
                }
            ]            
        }
    },    
    methods: {
        onSearch(){
            this.isSubmit = true
            this.results = this.domainList.filter(domainList => (domainList.name.toLowerCase()) == this.keyword.toLowerCase())
        },        
        onInput(){
            this.isSubmit = false
        },        
    }
}
</script>

<style lang="scss" src="./style.scss" scoped></style>