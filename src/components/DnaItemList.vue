<template>
<div>
    <table class="table">
        <thead class="thead">
            <tr>
                <th>Первая цепочка:</th>
                <th>Вторая цепочка:</th>
            </tr>
        </thead>
        <tbody>
            <tr
                v-for="(item, i) in firstChain"
                :key="item"
            >   
                <td><DnaItem
                    v-bind:item="item"
                /></td>
                <td class="container-td">
                    <div class="td-mod"></div>
                    <div class="td-mod"></div>
                </td>
                <td><DnaItem class="mirror" v-bind:revert="true" v-bind:item="secondChain[i]"/></td>
            </tr>
        </tbody>
    </table>
</div>
</template>

<script>
import DnaItem from '@/components/DnaItem'
export default {
    props: [
        'firstChain',
        'secondChain'
    ],
    components: {
        DnaItem
    }
}
</script>

<style scoped>
.table{
    width: 700px;
}
tr{
    display: flex;
    justify-content: center;
    flex-direction: row;
}
td{
    width: 300px;
}
.container-td{
    transition: opacity 0.5s ease;
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 30px;
    height: auto;
}
.td-mod{
    margin: 6px 0;
    align-self: center;
    width: 30px;
    border-top: 1px dashed black;
}
.mirror{
    transform: scale(-1, 1)
}
thead > tr{
    justify-content: space-around;
}
</style>