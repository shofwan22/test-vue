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
                />
                <button class="search__button">
                    <span class="icon-search"></span>
                    Search
                </button>
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
            
        }
    }
}
</script>

<style lang="scss" src="./style.scss" scoped></style>