<template>
    <input type="text"
        @input="handlerInput" 
    />
    <br>
    <span>{{ this.textFirstChain }}</span>
    <br>
    <span>{{ this.textSecondChain }}</span>
    <br>
    <span>{{ this.temperature }}</span>
    <br>
    <span>count A:{{ this.lengthA }}</span>
    <br>
    <span>count T:{{ this.lengthT }}</span>
    <br>
    <span>count G:{{ this.lengthG }}</span>
    <br>
    <span>count C:{{ this.lengthC }}</span>
</template>

<script>
export default {
    name: 'DnaCompnent',
    props: ['items'],
    components: {
        
    },
    methods: {
        handlerInput(e) {
            if (e.inputType == 'insertText') {
                let dataToLower = e.data.toLowerCase()
                if (dataToLower == "a" 
                || dataToLower == "t"
                || dataToLower == "g"
                || dataToLower == "c"
                ) {
                    if (this.textFirstChain.length < 100) {
                        this.textFirstChain += dataToLower
                        switch (dataToLower) {
                            case 'a':
                                this.textSecondChain += 't'
                                break;
                            case 't':
                                this.textSecondChain += 'a'
                                break;
                            case 'g':
                                this.textSecondChain += 'c'
                                break;
                            case 'c':
                                this.textSecondChain += 'g'
                                break;
                            default:
                                break;
                        }
                        if (this.textFirstChain.length < 14) 
                            this.calculateTemperature('first')
                        else
                            this.calculateTemperature('second')
                        
                    } else {
                        e.target.value = this.textFirstChain
                    }
                } else {
                    e.target.value = this.textFirstChain
                }
            } else if (e.inputType == 'deleteContentBackward') {
                this.textFirstChain = this.textFirstChain.slice(0, -1);
                this.textSecondChain = this.textSecondChain.slice(0, -1);
                if (this.textFirstChain.length < 14) 
                    this.calculateTemperature('first')
                else
                    this.calculateTemperature('second')
            }
            
        },
        calculateTemperature(type) {
            this.lengthA = this.textFirstChain != '' ? this.textFirstChain.match(/a/gm)?.length != undefined ? this.textFirstChain.match(/a/gm)?.length : 0 : 0
            this.lengthT = this.textFirstChain != '' ? this.textFirstChain.match(/t/gm)?.length != undefined ? this.textFirstChain.match(/t/gm)?.length : 0 : 0
            this.lengthG = this.textFirstChain != '' ? this.textFirstChain.match(/g/gm)?.length != undefined ? this.textFirstChain.match(/g/gm)?.length : 0 : 0
            this.lengthC = this.textFirstChain != '' ? this.textFirstChain.match(/c/gm)?.length != undefined ? this.textFirstChain.match(/c/gm)?.length : 0 : 0
            switch (type) {
                case 'first':
                    this.temperature = Math.round(2 * (this.lengthA + this.lengthT) + (this.lengthG + this.lengthC) * 4)
                    break;
                case 'second':
                    this.temperature = Math.round(64.9 + 41 * (this.lengthG + this.lengthC - 16.4) / (this.lengthA + this.lengthT + this.lengthG + this.lengthC))
                    break;
                default:
                    break;
            }
        }
    },
    data() {
        return {
            d: { RED: 'red', GREEN: 'green', BLUE: 'blue' },
            textFirstChain: '',
            textSecondChain: '',
            temperature: 0,
            lengthA: 0,
            lengthT: 0,
            lengthG: 0,
            lengthC: 0
        }
    }
}


</script>

<style scoped>
</style>