<template>
<div>
    <h2>Калькулятор ДНК</h2>
    <span>Введите последовательность нуклеотидов, состоящих из символов( a, t, g, c ):</span>
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
            let countA = 0
            let countT = 0
            let countG = 0
            let countC = 0
            for (let index = 0; index < this.textFirstChain.length; index++) {
                if (this.textFirstChain[index] == 'A') countA += 1
                if (this.textFirstChain[index] == 'T') countT += 1
                if (this.textFirstChain[index] == 'G') countG += 1
                if (this.textFirstChain[index] == 'C') countC += 1
            }
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
            comparison: {
                'A': 'T',
                'T': 'A',
                'G': 'C',
                'C': 'G'
            }
        }
    },
    updated() {
        this.textFirstChain = this.textFirstChain.toUpperCase()
        if (this.textFirstChain.match(/[^atgc]/gi)) {
            this.textFirstChain = this.textFirstChain.replace(/[^atgc]/gi ,'')
        } else {
            if (this.textFirstChain.length < 100) {
                this.textSecondChain = this.textFirstChain.split('').reduce((acc, element) => {
                    if(this.comparison[element]) return acc += this.comparison[element]
                }, '')
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