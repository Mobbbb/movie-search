<template>
    <Card class="search-list-wrap">
        <div class="empty-text" v-if="!params.length">请输入查询条件！</div>
        <div class="search-list" v-else>
            <div class="search-item" v-for="(item, index) in params" :key="`${index}1`">
                <img src="//www.baidu.com/img/flexible/logo/pc/result.png" class="image-preview">
                <div>电影名称</div>
                <div>起止时间</div>
            </div>
        </div>
    </Card>
</template>

<script>
export default {
    name: 'search-list',
    props: ['params'],
}
</script>

<style scoped>
    .search-list-wrap{
        margin: 24px 0;
        flex: 1;
        overflow-y: scroll;
        overflow-x: hidden;
    }
    .empty-text{
        text-align: center;
        font-size: 18px;
        margin-top: 208px;
    }
    .search-list{
        width: 100%;
        min-width: 1101px;
        height: 100%;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
    }
    .search-item{
        text-align: center;
        margin: 0 48px 24px 0;
    }
    .image-preview{
        width: 307px;
        height: 128px;
    }
</style>

<style>
    .search-list-wrap .ivu-card-body{
        height: 100%;
    }
</style>
