<template>
    <header>
        <h1>{{ text }}</h1>
        <Button
            v-show="homePage"
            :text="showAddTask ? 'Close' : 'Show'"
            :color="showAddTask ? 'red' : 'green'"
            @click="$emit('toggle-add-task')"
        />
    </header>
</template>

<script>
    import Button from './Button.vue';

    export default {
        name: 'Header',
        props: {
            text: String,
            showAddTask: Boolean,
        },
        components: {
            Button,
        },
        emits: ['toggle-add-task'],
        computed: {
            homePage(){
                if(this.$route.path === '/')
                    return true;
                return false;
            }
        }
    }
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>