<template>
    <Card class="search-list-wrap">
        <div class="empty-text" v-if="!params.length">
            <span v-if="isSearchResult">暂无数据！</span>
            <span v-else>请输入查询条件！</span>
        </div>
        <div class="search-list" v-else>
            <div class="search-item-wrap" v-for="(item, index) in params" :key="`${index}1`">
                <div class="search-item" v-if="item">
                    <img :src="item.image" class="preview-image">
                    <div class="item-title">电影名称：{{item.movieName}}</div>
                    <div class="item-time">起止时间: {{item.startTime}} - {{item.endTime}}</div>
                </div>
            </div>
        </div>
    </Card>
</template>

<script>
export default {
    name: 'search-list',
    props: ['params', 'isSearchResult'],
    mounted() {

    },
}
</script>

<style scoped>
    .search-list-wrap{
        margin: 24px 0;
        flex: 1;
        overflow-y: auto;
        overflow-x: hidden;
    }
    .empty-text{
        font-size: 18px;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        color: #595959;
    }
    .search-list{
        width: 100%;
        min-width: 1101px;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
    }
    .search-item-wrap{
        width: 307px;
        text-align: left;
        margin: 0 24px 24px 24px;
    }
    .search-item{
        
    }
    .search-item:hover{
        cursor: pointer;
    }
    .search-item:hover .item-time,.search-item:hover .item-title{
        color: #00a1d6;
    }
    .preview-image{
        width: 307px;
        height: 128px;
    }
    .item-title{
        transition: color .3s;
    }
    .item-time{
        color: #999;
        font-size: 12px;
        transition: color .3s;
    }
</style>

<style>
    .search-list-wrap .ivu-card-body{
        height: 100%;
    }
</style>
