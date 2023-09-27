<template>
    <!-- 地图 -->
    <div id="map">
        <LeftSider />
        <RightSider v-if="Object.keys(mapData).length" :mapData="mapData" />
    </div>
</template>

<script setup lang='ts'>
import { onMounted, ref } from "vue"

import AMapLoader from '@amap/amap-jsapi-loader';
import { Scene, PolygonLayer, LineLayer, Popup } from '@antv/l7';
import { GaodeMap } from '@antv/l7-maps';

import gaotang from '@/geojson/高唐城区.json'
import getRandomColor from '@/utils/getRandomColor'

import LeftSider from '@/components/LeftSider/LeftSider.vue'
import RightSider from '@/components/RightSider/RightSider.vue'

//地图数据
let mapData: any = ref({})

onMounted(() => {
    createMap()
})

function createMap() {
    AMapLoader.load({
        "key": "f8095f41557b132c958567ec784f9c1e",
        "version": "2.0",
        "plugins": [],
        "Loca": {
            "version": '2.0.0'
        },
    }).then((AMap) => {
        const map = new AMap.Map('map', {
            zoom: 10,
            zooms: [3, 20],
            center: [116.23560427568, 36.851591],
            viewMode: '3D'
        })
        const scene = new Scene({
            id: 'map',
            map: new GaodeMap({
                mapInstance: map,
            }),
            logoVisible: false,
        });
        mapData.value = {
            AMap,
            map,
            scene
        }
        drawPolygon(gaotang,scene)
    }).catch(e => {
        console.log(e);
    })
}
function drawPolygon(data: any, scene: any) {
    const layer = new PolygonLayer({
        name: 'firstLayer'
    })
        .source(data)
        .shape('fill')
        .color(getRandomColor())
        .style({
            opacity: 0.6,
        }).active(true);
    const layer2 = new LineLayer({
        zIndex: 2
    })
        .source(data)
        .color(getRandomColor())
        .active(true)
        .size(1)
    scene.addLayer(layer);
    scene.addLayer(layer2);
    let popup:any;
    //提示
    layer.on('mousemove', e => {
        const fieldArr: Array<any> = []
        let i = 0;
        //取前5个字段
        for (const field of Object.entries(e.feature.properties)) {
            if (i < 5) {
                fieldArr.push(field)
                i++
            }
        }
        const elementArr: Array<any> = []
        fieldArr.forEach(item => {
            elementArr.push(`
            <div style="display: flex;justify-content: space-between;">
            <span style="padding: 3px;">${item[0]}</span>
            <span style="padding: 3px;">${item[1]}</span>
        </div>
            `)
        })
        popup = new Popup({
            offsets: [0, 0],
            closeButton: false,
            anchor: ''
        })
            .setLnglat(e.lngLat)
            .setHTML(`
            <div>
                <div style="display: flex;justify-content: start;align-items: center;">
                    <svg viewBox="0 0 64 64" width="12px" height="12px" class="data-ex-icons-layers "
                        style="fill: grey;">
                        <path
                            d="M50.88,43.52a3.2,3.2,0,0,1,0,5.86L34.56,56.52a6.42,6.42,0,0,1-5.13,0L13.12,49.37a3.2,3.2,0,0,1,0-5.86l4.62-2a6,6,0,0,0,1.48,1l2.16.95-7,3.05,16.32,7.14a3.19,3.19,0,0,0,2.56,0L49.6,46.44l-7-3.05,2.16-.95a6,6,0,0,0,1.48-.95Zm0-14.39a3.2,3.2,0,0,1,0,5.86L34.56,42.13a6.42,6.42,0,0,1-5.13,0L13.12,35a3.2,3.2,0,0,1,0-5.86l4.62-2a6,6,0,0,0,1.48,1l2.16.95-7,3.05L30.72,39.2a3.19,3.19,0,0,0,2.56,0L49.6,32.06l-7-3.05,2.16-.95a6,6,0,0,0,1.48-.95ZM13.12,20.6a3.2,3.2,0,0,1,0-5.86L29.44,7.6a6.39,6.39,0,0,1,5.13,0l16.32,7.14a3.2,3.2,0,0,1,0,5.86L34.56,27.74a6.39,6.39,0,0,1-5.13,0Z">
                        </path>
                    </svg>
                    ${data.name}
                </div>
                ${elementArr.join('')}
            </div>
        `);
        scene.addPopup(popup);
    });
    //关闭提示
    layer.on('mouseout',()=>{
        if (popup) {  
        popup.remove();  
        popup = null;  
    }  
    })
    //将图层返回
    return layer;
}
</script>

<style lang="scss" scoped>
//地图
#map {
    width: 100vw;
    height: 100vh;
    position: relative;
    display: flex;
    align-items: center;
}
</style>
