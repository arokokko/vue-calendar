<template>
    <div class="week-row" >
        
        <app-day v-for="(day, index) in week"
             :day="day"
             :key="index"
        ></app-day>
    </div>
</template>
<script>
    
    import AppDay from './Day.vue';
    export default {
        components: {
            AppDay
        },
        data () {
            return {
                
            }
        },
    
        props:{
            week: {
                type: Array
            },
        },
        methods : {
            
        }
    }
</script>
<style>
    .week-row {
        width: 100%;
        border-left: 1px solid #e0e0e0;
        display: flex;
        cursor: pointer;
    }
    .week:nth-child(6),
    .week:nth-child(7) {
        color: rgba(51, 51, 51, .8)
    }
    
</style>