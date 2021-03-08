<template>
    <div class="Index">
        <div class="hearder-wrap">
            场景：<Input v-model="sceneText" placeholder="Enter scene..." class="header-input" />
            动作：<Input v-model="actionText" placeholder="Enter action..." class="header-input" />
            物体：<Input v-model="objectText" placeholder="Enter object..." class="header-input" />
            <Button class="header-button" @click="clear">清空</Button>
            <Button type="success" @click="search">搜索</Button>
        </div>
        <SearchList :params="searchList"/>
        <Page :total="searchList.length" show-elevator  v-if="searchList.length"/>
    </div>
</template>

<script>
import SearchList from '@/components/SearchList.vue';

export default {
    name: 'Index',
    components: {
        SearchList,
    },
    data() {
        return {
            sceneText: '',
            actionText: '',
            objectText: '',
            searchList: [],
        };
    },
    methods: {
        clear() {
             this.searchList = [];
        },
        search() {
            this.searchList = [1,2,2,2,2,2,2,2,2,2,2,2];
        },
    },
}
</script>

<style scoped>
    .Index{
        padding: 48px 68px 24px 68px;
        display: flex;
        flex-direction: column;
        height: 100%;
        box-sizing: border-box;
    }
    .hearder-wrap{
        white-space: nowrap;
        flex-shrink: 0;
    }
    .header-input{
        margin-right: 24px;
        width: 200px;
    }
    .header-button{
        margin: 0 24px 0 168px;
    }
</style>
