<template>
<div>
    <h2>Калькулятор ДНК</h2>
    <span>Введите последовательность нуклеотидов (состоящих из a, t, g, c символов):</span>
    <br>
    <input type="text"
        v-model="textFirstChain"
    />
    <button @click="handlerClickReset">сброс</button>
    <br>
    <span>Первая цепочка: {{ this.textFirstChain }}</span>
    <br>
    <span>Вторая цепочка: {{ this.textSecondChain }}</span>
    <br>
    <span>Температура плавления: {{ Math.round(this.temperature) }} °C ({{this.temperature.toFixed(4)}} °C)</span>
    <DnaItemList 
        v-bind:firstChain="textFirstChain"
        v-bind:secondChain="textSecondChain"
    />
</div>
</template>

<script>
import DnaItemList from '@/components/DnaItemList'
export default {
    name: 'DnaCompnent',
    props: ['items'],
    components: {
        DnaItemList
    },
    methods: {
        calculateTemperature(type) {
            let countA = this.textFirstChain != '' ? this.textFirstChain.match(/A/gm)?.length != undefined ? this.textFirstChain.match(/A/gm)?.length : 0 : 0
            let countT = this.textFirstChain != '' ? this.textFirstChain.match(/T/gm)?.length != undefined ? this.textFirstChain.match(/T/gm)?.length : 0 : 0
            let countG = this.textFirstChain != '' ? this.textFirstChain.match(/G/gm)?.length != undefined ? this.textFirstChain.match(/G/gm)?.length : 0 : 0
            let countC = this.textFirstChain != '' ? this.textFirstChain.match(/C/gm)?.length != undefined ? this.textFirstChain.match(/C/gm)?.length : 0 : 0
            switch (type) {
                case 'less':
                    this.temperature = 2 * (countA + countT) + (countG + countC) * 4
                    break;
                case 'over':
                    this.temperature = 64.9 + 41 * (countG + countC - 16.4) / (countA + countT + countG + countC)
                    break;
                default:
                    break;
            }
        },
        handlerClickReset() {
            this.textFirstChain = ''
        }
    },
    data() {
        return {
            type: { LESS14DEGREES: 'less', OVER14DEGREES: 'over' },
            textFirstChain: '',
            textSecondChain: '',
            temperature: 0,
            lengthA: 0,
            lengthT: 0,
            lengthG: 0,
            lengthC: 0
        }
    },
    updated() {
        this.textFirstChain = this.textFirstChain.toUpperCase()
        if (this.textFirstChain.match(/[^atgc]/gi)) {
            this.textFirstChain = this.textFirstChain.replace(/[^atgc]/gi ,'')
        } else {
            if (this.textFirstChain.length < 100) {
                this.textSecondChain = this.textFirstChain.split('').map(element => {
                    switch (element) {
                        case 'A':
                            return element.replace('A', 'T')  
                        case 'T':
                            return element.replace('T', 'A')  
                        case 'G':
                            return element.replace('G', 'C')  
                        case 'C':
                            return element.replace('C', 'G')  
                        default:
                            return
                    } 
                }).join('')
                if (this.textFirstChain.length < 14) 
                    this.calculateTemperature(this.type.LESS14DEGREES)
                else
                    this.calculateTemperature(this.type.OVER14DEGREES)
            } else {
                this.textFirstChain = this.textFirstChain.slice(0, -1)
            }
        }
    }
}
</script>

<style scoped>
</style>