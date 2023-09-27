<template>
    <div class="rightSider">
        <!-- 关闭当前面板 -->
        <el-tooltip v-if="isShowDualMap" class="box-item" effect="dark" content="关闭当前面板" placement="left">
            <div class="bUfghK active" @click="closePanel">
                <svg viewBox="0 0 64 64" width="18px" height="18px" class="data-ex-icons-delete "
                    style="fill: currentcolor;">
                    <g transform="translate(8, 8)">
                        <path
                            d="M31.5059707,24 L47.5987718,7.90719891 C48.1337427,7.37222791 48.1337427,6.50972364 47.5987718,5.97475264 L42.0252474,0.40122825 C41.4902764,-0.13374275 40.6277721,-0.13374275 40.0928011,0.40122825 L24,16.4940293 L7.90719891,0.40122825 C7.37222791,-0.13374275 6.50972364,-0.13374275 5.97475264,0.40122825 L0.40122825,5.97475264 C-0.13374275,6.50972364 -0.13374275,7.37222791 0.40122825,7.90719891 L16.4940293,24 L0.40122825,40.0928011 C-0.13374275,40.6277721 -0.13374275,41.4902764 0.40122825,42.0252474 L5.97475264,47.5987718 C6.50972364,48.1337427 7.37222791,48.1337427 7.90719891,47.5987718 L24,31.5059707 L40.0928011,47.5987718 C40.6277721,48.1337427 41.4902764,48.1337427 42.0252474,47.5987718 L47.5987718,42.0252474 C48.1337427,41.4902764 48.1337427,40.6277721 47.5987718,40.0928011 L31.5059707,24 Z">
                        </path>
                    </g>
                </svg>
            </div>
        </el-tooltip>
        <!-- 切换到双地图 -->
        <el-tooltip v-else class="box-item" effect="dark" content="切换到双地图视角" placement="left">
            <div class="bUfghK active" @click="changeDualMap">
                <svg viewBox="0 0 64 64" width="18px" height="18px" class="data-ex-icons-split "
                    style="fill: currentcolor;">
                    <g transform="translate(7.500000, 7.500000)">
                        <path
                            d="M19.5,47.4137931 C19.5,48.8421157 20.6192881,50 22,50 C23.3807119,50 24.5,48.8421157 24.5,47.4137931 L24.5,2.5862069 C24.5,1.15788427 23.3807119,0 22,0 C20.6192881,0 19.5,1.15788427 19.5,2.5862069 L19.5,47.4137931 Z">
                        </path>
                        <rect x="0" y="4" width="44" height="5" rx="2.5"></rect>
                        <rect transform="translate(2.500000, 24.500000) rotate(90.000000) translate(-2.500000, -24.500000) "
                            x="-18" y="22" width="41" height="5" rx="2.5"></rect>
                        <rect
                            transform="translate(41.500000, 25.000000) rotate(90.000000) translate(-41.500000, -25.000000) "
                            x="20.5" y="22.5" width="42" height="5" rx="2.5"></rect>
                        <rect x="0" y="41" width="44" height="5" rx="2.5"></rect>
                    </g>
                </svg>
            </div>
        </el-tooltip>
        <!-- 可见图层 -->
        <div class="visibleLevel" v-if="isShowDualMap">
            <div v-if="isShowVisibleLevelOption" class="visibleLevelOption">
                <div class="title">
                    <span>可见图层</span>
                    <svg viewBox="0 0 64 64" width="16px" height="16px" class="svgActive" @click="visibleLayer">
                        <g transform="translate(8,8)">
                            <path
                                d="M16.127688,49.4434399 L0.686714703,34.0024666 C-0.228904901,33.086847 -0.228904901,31.6023343 0.686714703,30.6867147 C1.12641074,30.2470187 1.72276655,30 2.34459065,30 L17.785564,30 C19.0804456,30 20.1301546,31.049709 20.1301546,32.3445907 L20.1301546,47.785564 C20.1301546,49.0804456 19.0804456,50.1301546 17.785564,50.1301546 C17.1637399,50.1301546 16.5673841,49.883136 16.127688,49.4434399 Z">
                            </path>
                            <path
                                d="M45.127688,19.4434399 L29.6867147,4.0024666 C28.7710951,3.086847 28.7710951,1.60233431 29.6867147,0.686714703 C30.1264107,0.247018663 30.7227665,-8.17124146e-14 31.3445907,-8.17124146e-14 L46.785564,-7.7547585e-14 C48.0804456,-7.7547585e-14 49.1301546,1.04970899 49.1301546,2.34459065 L49.1301546,17.785564 C49.1301546,19.0804456 48.0804456,20.1301546 46.785564,20.1301546 C46.1637399,20.1301546 45.5673841,19.883136 45.127688,19.4434399 Z"
                                transform="translate(39.065077, 10.065077) rotate(-180.000000) translate(-39.065077, -10.065077)">
                            </path>
                        </g>
                    </svg>
                </div>
                <!-- 可见图层展示栏 -->
                <div class="visibleLevelBottomContent">
                    <!-- 可见图层item -->
                    <div class="visibleLevelBottomContent_item" v-for="(item,index) in visibleLevelCheckList" :key="item.label">
                        <input type="checkbox" name="" :id="item.label" v-model="item.isChecked" class="noShow">
                        <label :for="item.label" class="checkbox_label" @click="switchVisibleLevel(index,item.isChecked)">
                            <span class="big_circle">
                                <span class="small_circle"
                                    :style="{ backgroundColor: item.isChecked ? '#d3d8e0' : '#29323c' }"></span>
                            </span>
                            <p>高唐县城</p>
                        </label>
                    </div>
                </div>
            </div>
            <el-tooltip v-else class="box-item" effect="dark" content="查看图层" placement="left">
                <div class="bUfghK active" @click="visibleLayer">
                    <svg viewBox="0 0 64 64" width="22px" height="22px" class="data-ex-icons-layers "
                        style="fill: currentcolor;">
                        <path
                            d="M50.88,43.52a3.2,3.2,0,0,1,0,5.86L34.56,56.52a6.42,6.42,0,0,1-5.13,0L13.12,49.37a3.2,3.2,0,0,1,0-5.86l4.62-2a6,6,0,0,0,1.48,1l2.16.95-7,3.05,16.32,7.14a3.19,3.19,0,0,0,2.56,0L49.6,46.44l-7-3.05,2.16-.95a6,6,0,0,0,1.48-.95Zm0-14.39a3.2,3.2,0,0,1,0,5.86L34.56,42.13a6.42,6.42,0,0,1-5.13,0L13.12,35a3.2,3.2,0,0,1,0-5.86l4.62-2a6,6,0,0,0,1.48,1l2.16.95-7,3.05L30.72,39.2a3.19,3.19,0,0,0,2.56,0L49.6,32.06l-7-3.05,2.16-.95a6,6,0,0,0,1.48-.95ZM13.12,20.6a3.2,3.2,0,0,1,0-5.86L29.44,7.6a6.39,6.39,0,0,1,5.13,0l16.32,7.14a3.2,3.2,0,0,1,0,5.86L34.56,27.74a6.39,6.39,0,0,1-5.13,0Z">
                        </path>
                    </svg>
                </div>
            </el-tooltip>
        </div>
        <!-- 3d地图 -->
        <el-tooltip class="box-item" effect="dark" :content="!isShow3D ? '3D地图' : '禁用3D地图'" placement="left">
            <div class="bUfghK active" @click="change3D">
                <svg viewBox="0 0 64 64" width="22px" height="22px" class="data-ex-icons-cube3d "
                    style="fill: currentcolor;">
                    <path d="M29.2,29.57,9.52,40.93V20a2.81,2.81,0,0,1,1.4-2.43L29.2,7.06Z"></path>
                    <path d="M32.08,34.38l21,10.82L33.4,56.56a2.78,2.78,0,0,1-2.8,0L12.12,45.91Z"></path>
                    <path d="M54.48,20v19.6L34.8,29.49V7.06L53.09,17.61A2.81,2.81,0,0,1,54.48,20Z"></path>
                </svg>
            </div>
        </el-tooltip>
        <div class="drawmap">
            <!-- 在地图上绘制 -->
            <el-tooltip class="box-item" effect="dark" content="在地图上绘制" placement="left">
                <div class="bUfghK active" @click="mapDraw">
                    <svg viewBox="0 0 24 25" width="22px" height="22px" class="data-ex-icons-draw-polygon "
                        style="fill: currentcolor;">
                        <path d="M5 6L13 2L22 9L21 23L2 17L5 6Z" stroke="currentColor" fill="transparent"
                            stroke-width="1.5">
                        </path>
                        <path
                            d="M10 11C10.5523 11 11 10.5523 11 10C11 9.44772 10.5523 9 10 9C9.44772 9 9 9.44772 9 10C9 10.5523 9.44772 11 10 11Z">
                        </path>
                        <path
                            d="M11.5 16C12.3284 16 13 15.3284 13 14.5C13 13.6716 12.3284 13 11.5 13C10.6716 13 10 13.6716 10 14.5C10 15.3284 10.6716 16 11.5 16Z">
                        </path>
                        <path
                            d="M15.5 12C16.3284 12 17 11.3284 17 10.5C17 9.67157 16.3284 9 15.5 9C14.6716 9 14 9.67157 14 10.5C14 11.3284 14.6716 12 15.5 12Z">
                        </path>
                        <path
                            d="M22 11C23.1046 11 24 10.1046 24 9C24 7.89543 23.1046 7 22 7C20.8954 7 20 7.89543 20 9C20 10.1046 20.8954 11 22 11Z">
                        </path>
                        <path
                            d="M21 25C22.1046 25 23 24.1046 23 23C23 21.8954 22.1046 21 21 21C19.8954 21 19 21.8954 19 23C19 24.1046 19.8954 25 21 25Z">
                        </path>
                        <path
                            d="M2 19C3.10457 19 4 18.1046 4 17C4 15.8954 3.10457 15 2 15C0.89543 15 0 15.8954 0 17C0 18.1046 0.89543 19 2 19Z">
                        </path>
                        <path
                            d="M13 4C14.1046 4 15 3.10457 15 2C15 0.89543 14.1046 0 13 0C11.8954 0 11 0.89543 11 2C11 3.10457 11.8954 4 13 4Z">
                        </path>
                        <path
                            d="M5 8C6.10457 8 7 7.10457 7 6C7 4.89543 6.10457 4 5 4C3.89543 4 3 4.89543 3 6C3 7.10457 3.89543 8 5 8Z">
                        </path>
                    </svg>
                </div>
            </el-tooltip>
            <!-- 左侧的导航 -->
            <div v-if="isShowDrawMapOption" class="drawmap_option">
                <div class="jixxhc" :class="drawmap_option_active === 0 && 'drawmap_option_active'"
                    @click="selectDrawGraph">
                    <svg viewBox="0 0 64 64" width="16px" height="16px" class="data-ex-icons-cursorclick "
                        style="fill: currentcolor;">
                        <g transform="scale(1.2, 1.2) translate(0, 2)">
                            <polygon points="22.5,11.1 27.6,43.9 35.3,37.3 43,49 48.8,45 41,33.2 49,28.3 ">
                            </polygon>
                            <path
                                d="M21.2,27.8C14.5,26.6,9.8,20.7,9.8,14c0-7.7,6.3-14,14-14s14,6.3,14,14c0,0.8-0.1,1.5-0.2,2.3l-2.5-0.4 c0.1-0.6,0.2-1.3,0.2-1.8c0-6.4-5.2-11.5-11.5-11.5S12.3,7.7,12.3,14c0,5.5,3.9,10.3,9.4,11.4L21.2,27.8z">
                            </path>
                        </g>
                    </svg>
                    选择
                </div>
                <div class="jixxhc" :class="drawmap_option_active === 1 && 'drawmap_option_active'" @click="drawPolygon">
                    <svg viewBox="0 0 22 18" width="16px" height="16px" class="data-ex-icons-polygon "
                        style="fill: currentcolor;">
                        <path fill-rule="evenodd" clip-rule="evenodd" d="M9 2L18 6L20 16L2 13L9 2Z" stroke="currentColor"
                            fill="transparent" stroke-width="1.5"></path>
                        <path fill-rule="evenodd" clip-rule="evenodd"
                            d="M9 4C10.1046 4 11 3.10457 11 2C11 0.89543 10.1046 0 9 0C7.89543 0 7 0.89543 7 2C7 3.10457 7.89543 4 9 4Z">
                        </path>
                        <path fill-rule="evenodd" clip-rule="evenodd"
                            d="M2 15C3.10457 15 4 14.1046 4 13C4 11.8954 3.10457 11 2 11C0.89543 11 0 11.8954 0 13C0 14.1046 0.89543 15 2 15Z">
                        </path>
                        <path fill-rule="evenodd" clip-rule="evenodd"
                            d="M20 18C21.1046 18 22 17.1046 22 16C22 14.8954 21.1046 14 20 14C18.8954 14 18 14.8954 18 16C18 17.1046 18.8954 18 20 18Z">
                        </path>
                        <path fill-rule="evenodd" clip-rule="evenodd"
                            d="M18 8C19.1046 8 20 7.10457 20 6C20 4.89543 19.1046 4 18 4C16.8954 4 16 4.89543 16 6C16 7.10457 16.8954 8 18 8Z">
                        </path>
                    </svg>
                    polygon
                </div>
                <div class="jixxhc" :class="drawmap_option_active === 2 && 'drawmap_option_active'" @click="drawRectangle">
                    <svg viewBox="0 0 22 16" width="16px" height="16px" class="data-ex-icons-rectangle "
                        style="fill: currentcolor;">
                        <rect x="2" y="2" width="18" height="12" stroke="currentColor" fill="transparent"
                            stroke-width="1.5"></rect>
                        <path fill-rule="evenodd" clip-rule="evenodd"
                            d="M2 4C3.10457 4 4 3.10457 4 2C4 0.89543 3.10457 0 2 0C0.89543 0 0 0.89543 0 2C0 3.10457 0.89543 4 2 4Z">
                        </path>
                        <path fill-rule="evenodd" clip-rule="evenodd"
                            d="M2 16C3.10457 16 4 15.1046 4 14C4 12.8954 3.10457 12 2 12C0.89543 12 0 12.8954 0 14C0 15.1046 0.89543 16 2 16Z">
                        </path>
                        <path fill-rule="evenodd" clip-rule="evenodd"
                            d="M20 16C21.1046 16 22 15.1046 22 14C22 12.8954 21.1046 12 20 12C18.8954 12 18 12.8954 18 14C18 15.1046 18.8954 16 20 16Z">
                        </path>
                        <path fill-rule="evenodd" clip-rule="evenodd"
                            d="M20 4C21.1046 4 22 3.10457 22 2C22 0.89543 21.1046 0 20 0C18.8954 0 18 0.89543 18 2C18 3.10457 18.8954 4 20 4Z">
                        </path>
                    </svg>
                    rectangle
                </div>
                <div v-if="isShowDualMapData" :class="drawmap_option_active === 3 && 'drawmap_option_active'" class="jixxhc"
                    @click="showOrHideGraph('hide')">
                    <svg viewBox="0 0 64 64" width="16px" height="16px" class="data-ex-icons-eyeseen "
                        style="fill: currentcolor;">
                        <path
                            d="M55.25,35v-.09a1.86,1.86,0,0,0-.49-1,36.15,36.15,0,0,0-5.05-5,31.92,31.92,0,0,0-13.19-7A21.09,21.09,0,0,0,28,21.8a26.07,26.07,0,0,0-7.4,2.73,40.33,40.33,0,0,0-9.88,7.63c-.54.56-1.07,1.12-1.56,1.73a1.92,1.92,0,0,0,0,2.56,36.09,36.09,0,0,0,5.05,5,31.89,31.89,0,0,0,13.19,7,21.05,21.05,0,0,0,8.51.12,26.06,26.06,0,0,0,7.41-2.73,40.37,40.37,0,0,0,9.88-7.63c.54-.56,1.07-1.12,1.56-1.73a1.84,1.84,0,0,0,.49-1v-.19s0-.06,0-.09,0-.06,0-.09,0-.08,0-.09M32,44.51a9.35,9.35,0,1,1,9.28-9.35A9.31,9.31,0,0,1,32,44.51">
                        </path>
                        <path d="M32,32.07a3.1,3.1,0,1,1-3.07,3.1A3.08,3.08,0,0,1,32,32.07"></path><svg viewBox="0 0 22 16"
                            width="16px" height="16px" class="data-ex-icons-rectangle " style="fill: currentcolor;">
                            <rect x="2" y="2" width="18" height="12" stroke="currentColor" fill="transparent"
                                stroke-width="1.5"></rect>
                            <path fill-rule="evenodd" clip-rule="evenodd"
                                d="M2 4C3.10457 4 4 3.10457 4 2C4 0.89543 3.10457 0 2 0C0.89543 0 0 0.89543 0 2C0 3.10457 0.89543 4 2 4Z">
                            </path>
                            <path fill-rule="evenodd" clip-rule="evenodd"
                                d="M2 16C3.10457 16 4 15.1046 4 14C4 12.8954 3.10457 12 2 12C0.89543 12 0 12.8954 0 14C0 15.1046 0.89543 16 2 16Z">
                            </path>
                            <path fill-rule="evenodd" clip-rule="evenodd"
                                d="M20 16C21.1046 16 22 15.1046 22 14C22 12.8954 21.1046 12 20 12C18.8954 12 18 12.8954 18 14C18 15.1046 18.8954 16 20 16Z">
                            </path>
                            <path fill-rule="evenodd" clip-rule="evenodd"
                                d="M20 4C21.1046 4 22 3.10457 22 2C22 0.89543 21.1046 0 20 0C18.8954 0 18 0.89543 18 2C18 3.10457 18.8954 4 20 4Z">
                            </path>
                        </svg>
                    </svg>
                    隐藏
                </div>
                <div v-else class="jixxhc" :class="drawmap_option_active === 3 && 'drawmap_option_active'"
                    @click="showOrHideGraph('show')">
                    <svg viewBox="0 0 64 64" width="16px" height="16px" class="data-ex-icons-eyeunseen "
                        style="fill: currentcolor;">
                        <path
                            d="M17.55,44.49a42.79,42.79,0,0,1-4.18-3.08,36.09,36.09,0,0,1-5.05-5,1.92,1.92,0,0,1,0-2.56c.49-.6,1-1.17,1.56-1.73a40.33,40.33,0,0,1,9.88-7.63,26.07,26.07,0,0,1,7.4-2.73,21.09,21.09,0,0,1,8.51.12,24.12,24.12,0,0,1,3.41,1L34.34,27.7a7.49,7.49,0,0,0-9.59,9.59Z">
                        </path>
                        <path
                            d="M23.14,47.37l5.73-5.73a7.49,7.49,0,0,0,9.82-9.82l6-6a42.78,42.78,0,0,1,4.18,3.09,36.15,36.15,0,0,1,5.05,5,1.86,1.86,0,0,1,.49,1V35s0,0,0,.09,0,.06,0,.09,0,.06,0,.09v.19a1.84,1.84,0,0,1-.49,1c-.49.6-1,1.17-1.56,1.73a40.37,40.37,0,0,1-9.88,7.63,26.06,26.06,0,0,1-7.41,2.73,21.05,21.05,0,0,1-8.51-.12A24.09,24.09,0,0,1,23.14,47.37Z">
                        </path>
                    </svg>
                    显示
                </div>
            </div>
        </div>
        <!-- 图例 -->
        <div class="legend">
            <!-- 显示图例 -->
            <el-tooltip class="box-item" effect="dark" content="显示图例" placement="left">
                <div v-show="isNormalLegend" class="bUfghK active" @click="showLegend">
                    <svg viewBox="0 0 64 64" width="22px" height="22px" class="data-ex-icons-legend "
                        style="fill: currentcolor;">
                        <path
                            d="M29.78,45.89v5.56H46.44V45.89Zm-11.11,0v5.56h5.56V45.89ZM29.78,34.78v5.56H46.44V34.78Zm-11.11,0v5.56h5.56V34.78ZM29.78,23.67v5.56H46.44V23.67Zm-11.11,0v5.56h5.56V23.67ZM29.78,12.56v5.56H46.44V12.56Zm-11.11,0v5.56h5.56V12.56ZM15.89,7H49.22A2.78,2.78,0,0,1,52,9.78V54.22A2.78,2.78,0,0,1,49.22,57H15.89a2.78,2.78,0,0,1-2.78-2.78V9.78A2.78,2.78,0,0,1,15.89,7Z">
                        </path>
                    </svg>
                </div>
            </el-tooltip>
            <!-- 左侧的导航 -->
            <div v-if="isShowLegend" class="legend_option" :class="{ legend_option_change: !isNormalLegend }">
                <div class="title">
                    <span>图例图层</span>
                    <svg v-if="isNormalLegend" viewBox="0 0 64 64" width="16px" height="16px" class="svgActive"
                        @click="isNormalLegend = false">
                        <path
                            d="M36 35.476V59a1 1 0 0 1-1 1h-6a1 1 0 0 1-1-1V35.476C21.103 33.696 16 27.453 16 20c0-8.836 7.163-16 16-16s16 7.164 16 16c0 7.453-5.103 13.697-12 15.476z">
                        </path>
                    </svg>
                    <svg v-else viewBox="0 0 64 64" width="16px" height="16px" class="svgActive"
                        @click="isNormalLegend = true">
                        <g transform="translate(8,8)">
                            <path
                                d="M16.127688,49.4434399 L0.686714703,34.0024666 C-0.228904901,33.086847 -0.228904901,31.6023343 0.686714703,30.6867147 C1.12641074,30.2470187 1.72276655,30 2.34459065,30 L17.785564,30 C19.0804456,30 20.1301546,31.049709 20.1301546,32.3445907 L20.1301546,47.785564 C20.1301546,49.0804456 19.0804456,50.1301546 17.785564,50.1301546 C17.1637399,50.1301546 16.5673841,49.883136 16.127688,49.4434399 Z">
                            </path>
                            <path
                                d="M45.127688,19.4434399 L29.6867147,4.0024666 C28.7710951,3.086847 28.7710951,1.60233431 29.6867147,0.686714703 C30.1264107,0.247018663 30.7227665,-8.17124146e-14 31.3445907,-8.17124146e-14 L46.785564,-7.7547585e-14 C48.0804456,-7.7547585e-14 49.1301546,1.04970899 49.1301546,2.34459065 L49.1301546,17.785564 C49.1301546,19.0804456 48.0804456,20.1301546 46.785564,20.1301546 C46.1637399,20.1301546 45.5673841,19.883136 45.127688,19.4434399 Z"
                                transform="translate(39.065077, 10.065077) rotate(-180.000000) translate(-39.065077, -10.065077)">
                            </path>
                        </g>
                    </svg>
                </div>
                <!-- 图例内容 -->
                <div class="legendContent">
                    <div class="legendContent_item" v-for="item in 2">
                        <div class="item_details">
                            <p>高唐城区</p>
                            <svg width="160" height="14">
                                <g transform="translate(0, 0)">
                                    <rect width="20" height="10" style="fill: rgb(255, 203, 153);"></rect><text x="28"
                                        y="9"></text>
                                </g>
                            </svg>
                            <svg width="160" height="14">
                                <g transform="translate(0, 0)">
                                    <rect width="20" height="10" style="fill: red;"></rect><text x="28" y="9"></text>
                                </g>
                            </svg>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang='ts'>
import { ref, onMounted, reactive } from "vue"
//引入右键菜单的dom
import rightDeleteItem from '@/utils/rightDeleteItem.js'

//获取传过来的map,AMap,scene
let { mapData } = defineProps(['mapData'])
const { map, AMap, scene, } = mapData

//是否是双地图
let isShowDualMap = ref(false)
//是否是3D地图
let isShow3D = ref(false)
//是否展示地图绘制的选项
let isShowDrawMapOption = ref(false)
//是否展示显示图例的选项
let isShowLegend = ref(false)
//是否显示地图绘制的线、面(注：只有点击绘制地图后才会显示，否则都不显示)
let isShowDualMapData = ref(true)
//是否展示显示图层的选项
let isShowVisibleLevelOption = ref(false)
//是否正在画
let isDraw = ref(false)
//是否正在编辑
let isRedact = ref(false)
//图例是否在正常位置
let isNormalLegend = ref(true)

//鼠标工具
let mouseTool: any = ref({})
//多边形编辑器
let PolygonEditor: any = ref({})
//矩形编辑器
let RectangleEditor: any = ref({})
//右键菜单
let contextMenu: any = ref({})

//绘画的类型
let drawType = ref('')
//覆盖物的数组
let graphArr: Array<any> = reactive([])
//绘制地图选项的激活状态 0 选择,1 多边形,2 矩形,3 显示隐藏
let drawmap_option_active = ref(0)
//右键鼠标坐标
let lnglat: any = ref({})
//图层选项的选择框
let visibleLevelCheckList = reactive([
    { label: '0', isChecked: true },
    { label: '1', isChecked: true },
    { label: '2', isChecked: true },
    { label: '3', isChecked: true },
    { label: '4', isChecked: true }
])

onMounted(() => {
    map.setPitch(0, true)
    initMap()
})

/**
 * 地图相关
 */
//初始化地图
function initMap() {
    AMap.plugin(["AMap.MouseTool", 'AMap.PolygonEditor', 'AMap.RectangleEditor'], () => {
        mouseTool.value = new AMap.MouseTool(map)
        PolygonEditor.value = new AMap.PolygonEditor(map)
        RectangleEditor.value = new AMap.RectangleEditor(map)
    })
    //创建右键菜单
    contextMenu.value = new AMap.ContextMenu()
    //过滤图层
    contextMenu.value.addItem(rightDeleteItem[0], () => { })
    //复制几何图形
    contextMenu.value.addItem(rightDeleteItem[1], () => { })
    //删除
    contextMenu.value.addItem(
        rightDeleteItem[2],
        () => {
            //最近的图形
            let nearestGraph = null;
            //最近的距离
            let nearestDistance = Infinity;
            for (let i = 0; i < graphArr.length; i++) {
                //找出多边形的中心
                function calculatePolygonCenter(polygon: Array<any>) {
                    let x = 0, y = 0;
                    let n = polygon.length;
                    for (let i = 0; i < n; i++) {
                        x += polygon[i]['lng'];
                        y += polygon[i]['lat'];
                    }
                    return [x / n, y / n];
                }
                let graph = graphArr[i];
                let center
                if (graph.className == 'Overlay.Rectangle') {
                    //获取矩形的中心点
                    center = graph.getCenter()
                } else {
                    //获取多边形的中心
                    center = calculatePolygonCenter(graph.getPath())
                }
                //获取右键坐标点到图形中心点的距离
                let distance = lnglat.value.distance(center)
                //找出距离右键坐标点距离最近的那个图形
                if (distance < nearestDistance) {
                    nearestGraph = graph;
                    nearestDistance = distance;
                }
            }
            //删除图形
            if (nearestGraph) {
                //关闭编辑器
                if (nearestGraph.className == 'Overlay.Rectangle') {
                    RectangleEditor.value.close()
                } else {
                    PolygonEditor.value.close()
                }
                nearestGraph.setMap(null);
                graphArr.splice(graphArr.indexOf(nearestGraph), 1);
            }
            isRedact.value = false
            //关闭右键菜单
            contextMenu.value.close();
        }
    );
    //开启右键菜单
    contextMenu.value.open(map)
    // 鼠标工具绘制覆盖物结束时触发此事件，obj对象为绘制出来的覆盖物对象。
    mouseTool.value.on('draw', (event: any) => {
        //多边形绘画结束
        if (event.obj.getPath().length > 2 && drawType.value === 'polygon') {
            repeatedEditor(PolygonEditor.value, event.obj)
        }
        //矩形绘画结束
        if (event.obj.getPath().length == 4 && drawType.value === 'rectangle') {
            repeatedEditor(RectangleEditor.value, event.obj)
        }
        isDraw.value = false
        //将覆盖物添加进数组
        graphArr.push(event.obj)
        //每次画完图都需要切换到选择
        selectDrawGraph()
        console.log(graphArr)
    });
}
//切换3D地图
function change3D() {
    isShow3D.value = !isShow3D.value
    if (isShow3D.value) {
        map.setPitch(40, true)
    } else {
        map.setPitch(0, true)
    }
}
//选择绘画的图形
function selectDrawGraph() {
    //绘画地图选项切换为选择 0
    drawmap_option_active.value = 0
    //关闭各自的编辑器
    RectangleEditor.value.close()
    PolygonEditor.value.close()
    //如果点击了图形，就开启编辑器
    map.on('click', (e: any) => {
        graphArr.forEach((item) => {
            //关闭各自的编辑器
            RectangleEditor.value.close()
            PolygonEditor.value.close()
            //点击位置有绘画的图形，就打开它的编辑器
            if (item.contains(e.lnglat)) {
                if (item.className == 'Overlay.Rectangle') {
                    RectangleEditor.value.setTarget(item)
                    RectangleEditor.value.open()
                } else {
                    PolygonEditor.value.setTarget(item)
                    PolygonEditor.value.open()
                }
            }
        })
    })
}
//画多边形
function drawPolygon() {
    drawmap_option_active.value = 1
    //关闭编辑
    PolygonEditor.value.close()
    RectangleEditor.value.close()
    //是否正在绘制
    if (isDraw.value) return
    repeatedOperation('polygon')
    console.log('开始画多边形')
    //开启鼠标画多边形模式。鼠标在地图上单击开始绘制多边形，鼠标左键双击或右键单击结束当前多边形的绘制
    mouseTool.value.polygon({
        strokeStyle: 'dashed',
        draggable: true,
        fillColor: '#daba84',
        fillOpacity: 0.1
    })
}
//画矩形
function drawRectangle() {
    drawmap_option_active.value = 2
    //关闭编辑
    PolygonEditor.value.close()
    RectangleEditor.value.close()
    //是否正在绘制
    if (isDraw.value) return
    repeatedOperation('rectangle')
    console.log('开始执行画矩形')
    //开启鼠标画矩形模式。鼠标在地图上拉框即可绘制相应的矩形
    mouseTool.value.rectangle({
        strokeStyle: 'dashed',
        draggable: true,
        fillColor: '#daba84',
        fillOpacity: 0.1
    })
}
/**
 * 绘画的重复赋值封装
 * @param type 画的类型
 */
function repeatedOperation(type: string) {
    isDraw.value = true
    drawType.value = type
}
/**
 * 对Editor重复操作的封装
 * @param editor 编辑器对象
 * @param coveringObj  覆盖物对象
 */
function repeatedEditor(editor: any, coveringObj: any) {
    // drawType.value = ''
    //关闭当前鼠标操作
    mouseTool.value.close(false);
    // 设置编辑对象  
    editor.setTarget(coveringObj);
    // 开始编辑对象
    editor.open();
    //正在编辑
    isRedact.value = true
    // 右键删除
    map.on('rightclick', (e: any) => {
        //拿到鼠标的坐标点
        lnglat.value = e.lnglat
        contextMenu.value.open(map, e.lnglat);
    });
}
/**
 * 绘画图形的显示和隐藏
 * @param type  显示还是隐藏 'hide' 'show'
 */
function showOrHideGraph(type: string) {
    drawmap_option_active.value = 3
    if (type == 'hide') {
        // 是否显示地图绘制的线、面
        isShowDualMapData.value = false
        graphArr.forEach(item => {
            item.hide()
        })
    } else {
        isShowDualMapData.value = true
        graphArr.forEach(item => {
            item.show()
        })
    }
}
//可见图层的切换
function switchVisibleLevel(index:number,checked:boolean){
    console.log(index,'可见图层',checked)
    if(checked){
        //显示
    }else {
        //隐藏
       const layer =  scene.getLayerByName('firstLayer');
       layer.hide()
       console.log('layer',layer)
    }
}

/**
 * 显示隐藏
 */
//切换到双地图 *****未完成****
function changeDualMap() {
    isShowDualMap.value = true
}
//可见图层
function visibleLayer() {
    isShowVisibleLevelOption.value = !isShowVisibleLevelOption.value
}
//关闭当前面板
function closePanel() {
    isShowDualMap.value = false
}
//地图绘制
function mapDraw() {
    isShowDrawMapOption.value = !isShowDrawMapOption.value
}
//显示图例
function showLegend() {
    isShowLegend.value = !isShowLegend.value
}
</script>

<style lang="scss" scoped>
//大盒子
.rightSider {
    top: 0;
    width: 56px;
    height: 216px;
    right: 0px;
    padding: 12px;
    z-index: 10;
    margin-top: 0px;
    position: absolute;
    display: grid;
    row-gap: 8px;
    justify-items: end;

    //图例
    .legend {
        position: relative;
    }

    // 绘制地图
    .drawmap {
        position: relative;

        //绘制地图的侧边栏
        .drawmap_option {
            padding: 0;
            margin: 0;
            top: 0px;
            width: 78px;
            height: 272.65px;
            display: flex;
            background-color: rgb(41, 50, 60);
            box-shadow: rgba(0, 0, 0, 0.16) 0px 6px 12px 0px;
            font-size: 12px;
            transition: all 0.8s ease 0s;
            margin-top: 6px;
            transform: translateX(calc(-50% + 20px));
            pointer-events: all;
            z-index: 1000;
            flex-direction: column;
            position: absolute;
            right: 32px;

            //侧边栏item
            .jixxhc {
                flex: 1;
                display: flex;
                color: rgb(106, 116, 133);
                align-items: center;
                flex-direction: column;
                justify-content: center;
                border: 1px solid transparent;
                background-color: rgb(41, 50, 60);
            }

            //绘制地图选项激活状态
            .drawmap_option_active {
                background-color: #3a4552;
                color: #e9e9ea;
            }

            //鼠标移动的高亮
            .jixxhc:hover {
                @extend .drawmap_option_active
            }
        }
    }

    //可见图层
    .visibleLevel {

        //可见图层选项
        .visibleLevelOption {
            background-color: rgb(36, 39, 48);
            z-index: 1;
            width: 184px;
            min-height: 132px;
            margin-left: -180px;

            .title {
                display: flex;
                justify-content: space-between;
                align-items: center;
                background-color: rgb(41, 50, 60);
                height: 32px;
                padding: 0px 12px;
                font-family: ff-clan-web-pro, "Helvetica Neue", Helvetica, sans-serif;
                font-size: 11px;
                color: rgb(255, 255, 255);
            }

            // 可见图层选项底部内容
            .visibleLevelBottomContent {
                min-height: 100px;
                display: flex;
                flex-direction: column;
                padding: 10px 0;

                // item
                .visibleLevelBottomContent_item {
                    width: 160px;
                    height: 16px;
                    display: flex;
                    margin: 12px 0 0 15px;

                    &:nth-child(1) {
                        margin-top: 0;
                    }

                    //label
                    .checkbox_label {
                        display: flex;
                        align-items: center;
                        position: relative;
                        vertical-align: middle;
                        font-size: 12px;
                        line-height: 16px;
                        color: rgb(240, 240, 240);
                        cursor: pointer;

                        .big_circle {
                            display: flex;
                            justify-content: center;
                            align-items: center;
                            width: 16px;
                            height: 16px;
                            border-radius: 50%;
                            background-color: #29323c;

                            .small_circle {
                                display: inline-block;
                                width: 8px;
                                height: 8px;
                                border-radius: 50%;
                                background-color: #d3d8e0;
                            }
                        }

                        p {
                            padding-left: 10px;
                        }
                    }
                }
            }
        }
    }

    //地图右侧小图标
    .bUfghK {
        position: relative;
        -webkit-box-align: center;
        align-items: center;
        cursor: pointer;
        display: inline-flex;
        font-size: 11px;
        font-weight: 500;
        font-family: ff-clan-web-pro, "Helvetica Neue", Helvetica, sans-serif;
        -webkit-box-pack: center;
        justify-content: center;
        letter-spacing: 0.3px;
        line-height: 14px;
        outline: 0px;
        text-align: center;
        transition: all 0.4s ease 0s;
        vertical-align: middle;
        opacity: 1;
        pointer-events: all;
        box-shadow: rgba(0, 0, 0, 0.16) 0px 6px 12px 0px;
        height: 32px;
        width: 32px;
        padding: 0px;
        border-radius: 0px;
        background-color: rgb(41, 50, 60);
        color: rgb(106, 116, 133);
        border: 0px;
    }

    //显示图例的侧边栏
    .legend_option {
        background-color: rgb(36, 39, 48);
        z-index: 1;
        position: absolute;
        top: 0;
        right: 40px;
        width: 184px;
        height: 132px;

        .title {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: rgb(41, 50, 60);
            height: 32px;
            padding: 0px 12px;
            font-family: ff-clan-web-pro, "Helvetica Neue", Helvetica, sans-serif;
            font-size: 11px;
            color: rgb(255, 255, 255);
        }

        //图例侧边栏的底部内容
        .legendContent {
            height: 100px;
            max-height: 192px;

            .legendContent_item {
                background-color: rgb(36, 39, 48);
                display: flex;
                justify-content: center;
                align-items: center;

                .item_details {
                    border-top: 1px solid #363c47;
                    flex: 1;
                    flex-direction: column;
                    justify-content: space-evenly;
                    align-items: flex-start;

                    p {
                        display: flex;
                        justify-content: start;
                        font-size: 12px;
                        padding-left: 10px;
                        color: rgb(160, 167, 180);
                        font-weight: 500;
                    }

                    p,
                    svg {
                        flex: 1;
                        height: 20.56px;
                    }
                }
            }
        }
    }

    .legend_option_change {
        top: 40vh;
        right: 0;
    }
}

//鼠标移动高亮
.active {
    & :hover {
        color: #f0f0f0;
    }
}

//选项弹框右侧svg的颜色变化
.svgActive {
    fill: #1fbad6;

    & :hover {
        fill: #a0a7b4;
    }
}

//隐藏dom
.noShow {
    display: none;
}

//右键菜单item
.rightDelete {
    background-color: rgb(41, 50, 60);
    color: rgb(157, 164, 177);
    display: flex;
    justify-content: space-around;
    align-items: center;
    font-size: 12px;
    line-height: 14px;
    padding: 8px;
    text-transform: capitalize;

    div,
    span {
        display: flex;
        margin-left: 6px;
    }
}

.amap-menu {
    .amap-menu-outer {
        li {
            padding: 0 !important;
        }
    }
}
</style>
