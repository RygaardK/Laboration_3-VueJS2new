<template>
    <div id="header">
        <Upload v-on:inputData="sendData($event)" /> 
    </div>
</template>

<script>
import Upload from './Upload'

export default {
    name: 'Header',
    components: {
        "Upload": Upload
    },
    props: {
        inputData: Array,
    },
    data() {
        return{
            title: '',
            content: ''
        }

    },
    methods: {
        sendData: function(inputData){
            this.$emit('sendData', inputData)
            console.log('(HEADER)This is sendData: ', inputData)
        }
    }
}

</script>


<style scoped>


</style>