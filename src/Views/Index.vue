<template>
    <div class="Index">
        <div class="header-wrap">
            场景：<Input v-model="sceneText" placeholder="Enter scene..." class="header-input" />
            动作：<Input v-model="actionText" placeholder="Enter action..." class="header-input" />
            物体：<Input v-model="objectText" placeholder="Enter object..." class="header-input" />
            <Button class="header-button" @click="clear">清空</Button>
            <Button type="success" @click="search">搜索</Button>
        </div>
        <SearchList :params="showSearchList" :isSearchResult="isSearchResult" />
        <Page :page-size="pageSize" :total="total" show-elevator v-if="total" @on-change="changePage" />
    </div>
</template>

<script>
import SearchList from '@/components/SearchList.vue';

const movieName1 = 1291543;
const movieName2 = 1291544;
const sceneData = {}
const actionData = {};
const objectData = {};

sceneData[movieName1] = require('@/mock/场景/' + movieName1 + '.json').shot;
sceneData[movieName2] = require('@/mock/场景/' + movieName2 + '.json').shot;
actionData[movieName1] = require('@/mock/动作/' + movieName1 + '.json').shot;
actionData[movieName2] = require('@/mock/动作/' + movieName2 + '.json').shot;
objectData[movieName1] = require('@/mock/物体/' + movieName1 + '.json').shot;
objectData[movieName2] = require('@/mock/物体/' + movieName2 + '.json').shot;

export default {
    name: 'Index',
    components: {
        SearchList,
    },
    data() {
        return {
            page: 1,
            pageSize: 12,
            sceneText: '',
            actionText: '',
            objectText: '',
            allSearchList: [], // 筛选出的符合条件的列表集合
            isSearchResult: false, // 此次搜索输入框是否有内容输入
        };
    },
    computed: {
        showSearchList() { // 当前页展示的列表集合
            if (this.allSearchList.length && this.searchAble) {
                let resultList = this.allSearchList.slice((this.page - 1) * this.pageSize, this.page * this.pageSize);
                const restNum = this.pageSize - resultList.length;
                if (restNum > 0) {
                    resultList = resultList.concat(Array.from({ length: restNum }, () => 0))
                }
                return resultList;
            }
            return [];
        },
        searchAble() {
            return this.sceneText || this.actionText || this.objectText;
        },
        total() { // 总条数
            return this.allSearchList.length;
        },
    },
    methods: {
        /**
         * @description 翻页
         */
        changePage(page) {
            this.page = page;
        },
        /**
         * @description 清空
         */
        clear() {
            this.sceneText = '';
            this.actionText = '';
            this.objectText = '';
            this.allSearchList = [];
            this.isSearchResult = false;
        },
        /**
         * @description 搜索
         */
        search() {
            this.page = 1;
            this.allSearchList = [];
            this.isSearchResult = this.sceneText || this.actionText || this.objectText;
            this.getAllSearchListByIndex(sceneData, this.sceneText);
            this.getAllSearchListByIndex(actionData, this.actionText);
            this.getAllSearchListByIndex(objectData, this.objectText);
        },
        getAllSearchListByIndex(jsonData, searchIndex) {
            if (searchIndex) {
                let key, shotItem, searchKey;
                Object.keys(jsonData).forEach(movieName => {
                    jsonData[movieName].forEach(item => {
                        key = Object.keys(item)[0];
                        shotItem = item[key];
                        searchKey = JSON.stringify(shotItem[2]);
                        if (searchKey.indexOf(searchIndex) > -1) {
                            // 构造待展示的列表数据
                            this.allSearchList.push({
                                movieName,
                                image: `http://${location.hostname}:8088/${movieName}/shot_${key}_img_1.jpg`, // 图片地址
                                startTime: this.formatTime(shotItem[0]), // 开始时间
                                endTime: this.formatTime(shotItem[1]), // 结束时间
                            });
                        }
                    });
                });
            }
        },
        /**
         * @description 时间格式化
         * @param time
         * @returns {string}
         */
        formatTime(time) {
            let secondsNum = Number(time).toFixed(0);
            let minutes = Math.floor(secondsNum / 60);
            let seconds = secondsNum % 60;

            minutes = minutes < 10 ? `0${minutes}` : minutes;
            seconds = seconds < 10 ? `0${seconds}` : seconds;

            return `${minutes}:${seconds}`;
        },
    },
}
</script>

<style scoped>
    .Index{
        padding: 48px 68px 68px 68px;
        display: flex;
        flex-direction: column;
        height: 100%;
        box-sizing: border-box;
        color: #262626;
        font-size: 14px;
    }
    .header-wrap{
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
