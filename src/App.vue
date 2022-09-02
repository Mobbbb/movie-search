<template>
    <div id="app">
        <!--<Index />-->
        <template v-for="item in circleMapX">
            <div class="point-wrap" :key="item + '1'">
                <div class="point" v-for="cell in circleMapY" :key="cell" :value="item + ',' + cell"></div>
            </div>
        </template>
        {{successTimes / totalTimes}}
    </div>
</template>

<script>
import Index from './Views/Index.vue'
import bluePoints from './arr'

export default {
    name: 'App',
    components: {
        Index
    },
    data () {
        return {
            circleMapX: 100,
            circleMapY: 100,
            centerPointer: [50, 50],
            R: 50,
            totalTimes: 0,
            successTimes: 0,
        }
    },
    mounted() {
        /*const points = document.getElementsByClassName('point')
        points.forEach(item => {
            let pointXY = item.getAttribute('value').split(',')
            let X = pointXY[0] - this.centerPointer[0]
            let Y = pointXY[1] - this.centerPointer[1]
            let sqrtXY = Math.sqrt(X * X + Y * Y)
            if (sqrtXY < this.R) {
                item.classList.add('blue')
            }
        });
        const bluePoints = document.getElementsByClassName('blue')

        let arr = []
        bluePoints.forEach(item => {
            arr.push(item.getAttribute('value').split(','))
        })*/
        
        setInterval(() => {
            let A = bluePoints[Math.floor(Math.random() * (bluePoints.length - 1 + 1))]
            let B = bluePoints[Math.floor(Math.random() * (bluePoints.length - 1 + 1))]
            let C = bluePoints[Math.floor(Math.random() * (bluePoints.length - 1 + 1))]
            let D = bluePoints[Math.floor(Math.random() * (bluePoints.length - 1 + 1))]

            let ABC = this.isInTriangle(A[0], A[1], B[0], B[1], C[0], C[1])
            let ABD = this.isInTriangle(A[0], A[1], B[0], B[1], D[0], D[1])
            let ACD = this.isInTriangle(A[0], A[1], C[0], C[1], D[0], D[1])
            let BCD = this.isInTriangle(B[0], B[1], C[0], C[1], D[0], D[1])

            this.totalTimes ++
            if (ABC && ABD && ACD && BCD) {
                this.successTimes ++
            }
        }, 50000)
        
    },
    methods: {
        isInTriangle(x1, y1, x2, y2, x3, y3) {
            let x0 = this.centerPointer[0]
            let y0 = this.centerPointer[1]

            let s0 = this.getRound(x1, y1, x2, y2, x3, y3)
            let s1 = this.getRound(x1, y1, x2, y2, x0, y0)
            let s2 = this.getRound(x2, y2, x3, y3, x0, y0)
            let s3 = this.getRound(x1, y1, x3, y3, x0, y0)

            let result = s0 - s1 - s2 - s3

            return result > -0.1 || result < 0.1
        },
        getRound(x1, y1, x2, y2, x3, y3) {
            let a = Math.sqrt((x1 - x2) * (x1 - x2) + (y1 - y2) * (y1 - y2))
            let b = Math.sqrt((x1 - x3) * (x1 - x3) + (y1 - y3) * (y1 - y3))
            let c = Math.sqrt((x2 - x3) * (x2 - x3) + (y2 - y3) * (y2 - y3))

            let p = (a + b + c) / 2
            
            return Math.sqrt(p * (p - a) * (p - b) * (p - c))
        },
    },
}
</script>

<style>
    html,body{
        height: 100%;
    }
    #app{
        height: 100%;
    }
    .point-wrap{
        display: flex;
        justify-content: center;
    }
    .point{
        height: 1px;
        width: 1px;
        background: white;
    }
    .blue{
        background: blue;
    }
</style>
