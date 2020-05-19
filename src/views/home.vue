<template>
  <div class="index_home">
    <!--header-->
    <div class="header">
      <div class="bg_header">
        <div class="header_nav fl t_title">
          <img src="static/img/jh2.png" style="width: 80px;height: 90px;float: left;margin-left: 38%;" alt="图片加载中......">
          <div style="margin-left: 10px;float: left;">
            网络反欺诈平台
          </div>
        </div>
      </div>
    </div>

    <!--  content  -->
    <div class="data_content">
      <div class="data_time">
        <div style="display: inline-block;margin-right: 12%;margin-left: 25px;">
          累计发现危害网站:
          <span class="data_number">105822</span>
          个
        </div>
        <div style="display: inline-block;">
          提醒危害网站累计次数:
          <span class="data_number">10362822</span>
          个
        </div>
        <div style="display: inline-block;margin-left: 12%;">
          单日提醒危害网站个数:
          <span class="data_number">68974</span>
          个
        </div>
      </div>

      <div class="data_main">
        <div class="main_left fl">

          <div class="left_1 t_btn6">

            <div class="main_title">
              实时提醒量
            </div>

            <hr width="92%" color="#00DA78" style="margin: 0 auto;">
            <echart style="height: 300px;" :id="'ss_chart'" :data="[1]" :option-data="ssoption"></echart>
          </div>

          <div class="left_2">
            <div class="main_table t_btn2">
              <table>
                <thead>
                <tr>
                  <th>时间</th>
                  <th>来源</th>
                  <th>IP</th>
                  <th>域名</th>
                  <th>仿冒</th>
                </tr>
                </thead>
                <tbody>
                <tr>
                  <td>2020-05-01 12:24:06</td>
                  <td>深圳</td>
                  <td>192.168.1.1</td>
                  <td>www.fsj765.com</td>
                  <td>仿冒公司</td>
                </tr>
                <tr>
                  <td>2020-02-01 12:24:06</td>
                  <td>深圳</td>
                  <td>128.168.13.2</td>
                  <td>www.baibailei.com</td>
                  <td>仿冒公司</td>
                </tr>
                <tr>
                  <td>2020-03-01 12:24:06</td>
                  <td>深圳</td>
                  <td>79.136.12.33</td>
                  <td>156.36.2.65</td>
                  <td>仿冒公司</td>
                </tr>
                <tr>
                  <td>2020-04-01 12:24:06</td>
                  <td>深圳</td>
                  <td>166.36.32.66</td>
                  <td>www.heidalao.com</td>
                  <td>仿冒公司</td>
                </tr>
                <tr>
                  <td>2020-05-01 12:24:06</td>
                  <td>深圳</td>
                  <td>182.54.56.32</td>
                  <td>174.162.35.6</td>
                  <td>仿冒公司</td>
                </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <div class="main_center fl">
          <div class="center_text">
            <!--            地图-->
            <div id="chart" style="width: 98%;height: 690px;margin-top: 5px;margin-left: 1%;"></div>
<!--            <iframe src="/static/map/demo01.html" frameborder="0" width="100%" height="690px" scrolling="no"></iframe>-->
<!--            <echart style="height: 690px;" :id="'map_chart'" :data="[1]" :option-data="mapOption"></echart>-->
<!--            <div id='MapBox'>-->
<!--              <div class='baiduMap' id='mapShow'></div>-->
<!--            </div>-->
          </div>
        </div>

        <div class="main_right fr">
          <div class="right_1">
            <div class="main_title">
              各类网站提醒数量占比
            </div>

            <hr width="92%" color="#00DA78" style="margin: 0 auto;">

            <echart style="height: 300px;" :id="'web_chart'" :data="[1]" :option-data="webOption"></echart>
          </div>
          <div class="right_2">
            <div class="main_title">
              终端提醒数量占比
            </div>

            <hr width="92%" color="#00DA78" style="margin: 0 auto;">

            <echart style="height: 300px;" :id="'region_chart'" :data="[1]" :option-data="regionOption"></echart>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import echart from '@/components/charts/index';
  import echarts from 'echarts';
  //引入json数据
  import baiduJSON from './baiduData';
  import styleJSON from '../../static/map/map_config';
  import shenzhen from 'echarts/map/json/province/shenzhen';
  import shanghai from 'echarts/map/json/province/shanghai';
  import '../../static/map/map_load';

    export default {
        name: "home",
        components: {
          echart
        },
        data (){
          return {
            ssoption: {
              xAxis: {
                type: 'category',
                boundaryGap: false,
                data: ['02', '04', '06', '08', '10', '12', '14']
              },
              grid: {
                top: '11%',
                left: '6%',
                right: '8%',
                bottom: '12%',
                containLabel: true
              },
              yAxis: {
                type: 'value'
              },
              textStyle: {
                color: '#fff'
              },
              series: [{
                data: [28898, 30010, 23156, 11469, 25893, 55436, 43219],
                type: 'line',
                areaStyle: {}
              }]
            },
            webOption: {
              tooltip: {
                trigger: 'item',
                formatter: '{a} <br/>{b}: {c} ({d}%)'
              },
              legend: {
                orient: 'vertical',
                left: 8,
                top: 5,
                data: ['信息诈骗', '博彩网站', '恶意文件', '社工欺诈', '虚假销售'],
                textStyle: {
                  color: '#fff',
                  fontSize: 15
                },
              },
              series: [
                {
                  name: '网站类型',
                  type: 'pie',
                  radius: ['40%', '55%'],
                  avoidLabelOverlap: false,
                  label: {
                    show: false,
                    position: 'center'
                  },
                  center: ['60%', '50%'],
                  emphasis: {
                    label: {
                      show: true,
                      fontSize: '24',
                      fontWeight: 'bold'
                    }
                  },
                  labelLine: {
                    show: false
                  },
                  color: ['#00C6E4', 'green', '#f18341', 'red', '#F14A00'],
                  data: [
                    {value: 335, name: '信息诈骗'},
                    {value: 1548, name: '博彩网站'},
                    {value: 234, name: '恶意文件'},
                    {value: 135, name: '社工欺诈'},
                    {value: 348, name: '虚假销售'}
                  ]
                }
              ]
            },
            regionOption: {
              tooltip: {
                trigger: 'item',
                formatter: '{a} <br/>{b}: {c} ({d}%)'
              },
              legend: {
                orient: 'vertical',
                left: 8,
                top: 5,
                data: ['移动端', 'PC端'],
                textStyle: {
                  color: '#fff',
                  fontSize: 15
                },
              },
              series: [
                {
                  name: '网站类型',
                  type: 'pie',
                  radius: ['40%', '55%'],
                  avoidLabelOverlap: false,
                  label: {
                    show: true,
                    position: 'outside'
                  },
                  center: ['60%', '50%'],
                  emphasis: {
                    label: {
                      show: true,
                      fontSize: '24',
                      fontWeight: 'bold'
                    }
                  },
                  labelLine: {
                    show: true
                  },
                  color: ['red', '#00C6E4', '#f18341', 'green', '#F14A00'],
                  data: [
                    {value: 423, name: '移动端'},
                    {value: 355, name: 'PC端'}
                  ]
                }
              ]
            },
            mapOption: {
              series: [{
                type: 'map',
                map: '上海'
              }]
            }
          }
        },
      methods: {
        baiduMap:function(){
          var me=this;
          me.map = new BMap.Map("mapShow")
          var point = new BMap.Point(114.065537,22.553321);  // 创建点坐标
          me.marker=new BMap.Marker(point);
          me.overView=new BMap.OverviewMapControl({isOpen: true});//缩略地图控件。
          me.map.addControl(me.overView);
          me.map.addOverlay(me.marker);//添加一个标注
          me.map.centerAndZoom(point, 13);                 // 初始化地图，设置中心点坐标和地图级别
          me.map.enableScrollWheelZoom(true);     //开启鼠标滚轮缩放
        }
      },
      mounted() {
        // echarts.registerMap('深圳', shenzhen);
        let myChart = echarts.init(document.getElementById('chart'));
        let pointsData = baiduJSON;//其实这一步是多余的
        //把数据处理成需要的格式，只是把数值都改成了1，具体项目可以根据自己实际来处理
        var points = [].concat.apply([], pointsData.map(function (track) {
          return track.map(function (seg) {
            return seg.coord.concat([1]);
          });
        }));
        // this.mapOption.series[1].data = points;
        let option;
        myChart.setOption(option = {
          animation: false,
          bmap: {
            // center: [120.13066322374, 30.240018034923],
            center: [113.82064, 22.64343],
            zoom: 14,
            roam: true
            // mapStyle: {style:'midnight'}
          },
          visualMap: {
            show: false,
            top: 'top',
            min: 0,
            max: 5,
            seriesIndex: 0,
            calculable: true,
            inRange: {
              color: ['blue', 'blue', 'green', 'yellow', 'red']
            }
          },
          series: [{
            type: 'heatmap',
            coordinateSystem: 'bmap',
            data: points,
            pointSize: 5,
            blurSize: 6
          }]
        });
        var bmap = myChart.getModel().getComponent('bmap').getBMap();

        // 设置最小缩放值
        bmap.setMinZoom(11);
        // 设置最大缩放值
        bmap.setMaxZoom(15);

        // var b = new BMap.Bounds(new BMap.Point(116.027143, 39.772348),new BMap.Point(116.832025, 40.126349));

        // try {
        //   BMapLib.AreaRestriction.setBounds(map, b);
        // } catch (e) {
        //   alert(e);
        // }

        bmap.addControl(new BMap.MapTypeControl());

        // this.baiduMap();
      }
    }
</script>

<style scoped>
  @import "../static/css/index.scss";

  *{
    margin: 0;
    padding: 0;
    font-family: PingFangSC-Light, 微软雅黑;
  }
  .t_title{
    width: 100%;
    height: 100%;
    font-size: 3.3em;
    line-height: 100px;
    color: #00DA78;
  }
  .index_home{
    width: 100%;
    height: auto;
    color:#333;
     /*overflow: hidden;*/
    background: url('/static/img/true.png') no-repeat;
    background-size: 100% 100%;
  }
  .BMap_cpyCtrl {
    display: none !important;
  }
  .anchorBL {
    display: none !important;
  }
  .data_number {
    font-size: 32px;
    color: #fff;
  }

  #MapBox {
    width: 100%;
    height: 100%;
    padding: 10px;
    position: relative;
  }
  /* 地图 */
  .baiduMap{
    height: 100%;
    width: 100%;
  }

</style>
