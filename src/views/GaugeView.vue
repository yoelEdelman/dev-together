<template>
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
        <div class="mx-auto max-w-3xl">
            <div class="m-auto flex justify-center content-center" id="gaugeArea"></div>
            <span class="isolate inline-flex rounded-md shadow-sm">
                <button @click="reduce" type="button" class="relative inline-flex items-center rounded-l-md border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-1 focus:ring-indigo-500">-</button>
                <input @change="adjust" type="text" class="text-center relative -ml-px inline-flex items-center border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-1 focus:ring-indigo-500" v-model="visibleValue">
                <button @click="increase" type="button" class="relative -ml-px inline-flex items-center rounded-r-md border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-1 focus:ring-indigo-500">+</button>
            </span>
        </div>
    </div>
</template>


<script>
import {gaugeChart} from "gauge-chart";
export default {
    name: 'GaugeView',
    data() {
        return {
            element: '',
            value: 50,
            visibleValue: 100,
            gaugeOptions: {
                hasNeedle: true,
                needleColor: 'black',
                needleUpdateSpeed: 0,
                arcColors: ['red', 'yellow', 'green'],
                arcDelimiters: [33,66,99.9],
                rangeLabel: ['0', '200'],
            }
        }
    },
    mounted() {
        this.element = document.querySelector('#gaugeArea')
        gaugeChart(this.element, 300, this.gaugeOptions).updateNeedle(this.value)
    },
    methods : {
        increase: function () {
            this.visibleValue++
            this.updateChart()
        },
        reduce: function () {
            this.visibleValue--
            this.updateChart()
        },
        adjust: function () {
            this.updateChart()
        },
        updateChart: function () {
            this.value = this.visibleValue / 2
            this.element.innerHTML = ''
            gaugeChart(this.element, 300, this.gaugeOptions).updateNeedle(this.value)
        }
    }
}
</script>
