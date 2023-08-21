<template>
    <header>
        <h1>{{ title }}</h1>
        <MainButton @btn-click="$emit('toggle-add-task')" :text="showAddTask ? 'Close' : 'Add'" :color="showAddTask ? 'red' : 'green'"/>
    </header>
</template>

<script>
import MainButton from './Button'


export default {
    name: "MainHeader",
    props: {
        title: String,
        showAddTask: Boolean

    },
    components: {
        MainButton,        
    },
    methods: {
        onClick(){
            console.log('click')
        },
    }
};
</script>



<style scoped>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>
