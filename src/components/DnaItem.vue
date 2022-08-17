<template>
    <li>{{ item.title }}</li>
</template>

<script>
export default {
    name: 'DnaItem',
    props: {
      item: {
        type: Object,
        required: true
      } 
    }
}

</script>