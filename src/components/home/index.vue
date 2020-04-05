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
            <p v-if="isEmpty" class="empty">Sorry, domain isn't available</p>

            <div v-if="showRecommendation" class="recommendation">
                <div v-for="(recommendation,index) in recommendations" :key="index" class="recommendation__list">
                    <p class="recommendation__list__name">{{ recommendation.name }}</p>
                    <p class="recommendation__list__price">{{ recommendation.price }}</p>
                    <button v-if="!recommendation.status" class="recommendation__list__buy" @click="onClickBuy(recommendation)">Buy</button>
                    <span v-else class="recommendation__list__purchased">Purchased</span>
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
    computed: {
        isEmpty(){
            return (this.keyword != '') && (this.results.length == 0) && (this.isSubmit == true)
        },
        showRecommendation(){
            return (this.recommendations.length > 0) && (this.results.length == 0)
        }
    },    
    methods: {
        onSearch(){
            this.isSubmit = true
            this.results = this.domainList.filter(domainList => (domainList.name.toLowerCase()) == this.keyword.toLowerCase())
            this.getRecommendation()
        },
        getRecommendation(){
            if(this.keyword != ''){
                this.recommendations = this.domainList.filter(domainList => (domainList.name.toLowerCase()).includes(this.keyword.toLowerCase()))
            }else{
                this.recommendations = []
            }
        },        
        onInput(){
            this.isSubmit = false
        },
        onClickBuy(data){
            data.status = true
        }        
    }
}
</script>

<style lang="scss" src="./style.scss" scoped></style>