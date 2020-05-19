<template>
    <div :id="id" style="width: 100%;height: 100%"></div>
</template>

<script>
    import echarts from 'echarts';
    import 'echarts/extension/bmap/bmap';
    import china from 'echarts/map/js/china';
    import world from 'echarts/map/js/world';
    import shenzhen from 'echarts/map/json/province/shenzhen';
    import shanghai from 'echarts/map/json/province/shanghai';
    import sz from 'echarts/map/json/sz';

    export default {
        name: "index",
        props: {
            id: {
                type: String,
                required: true
            },
            data: Array,
            optionData: Object
        },
        data(){
            return {
                myChart: null,
                option: null
            }
        },
        watch: {
            "data": function () {
                this.renderCharts();
            }
        },
        methods: {
            renderCharts() {
                // console.log(this.myChart);
                // console.log(this.optionData);
                if (!this.myChart) {
                    this.myChart = echarts.init(document.getElementById(this.id));
                }
                this.option = this.optionData || {};
                if (this.option != {}) {
                    this.myChart.setOption(this.option, true);
                }
            },
        },
        mounted() {
            this.renderCharts();
            var that=this;
            window.addEventListener('resize', function () {
                that.myChart.resize();
            });
        },
        // 离开时销毁 window.onresize 事件
        beforeDestroy() {
            window.onresize = null;
        }
    }
</script>

<style scoped>

</style>
