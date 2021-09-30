<template>
    <div class="row">
        
        <div class="col-sm-6 header">
                <button @click.stop="goPrev" class="btn ">&#60;</button>
                <div class="title"> {{title}}</div>
                <button @click.stop="goNext" class="btn ">&#62;</button>
            
        </div>
        
    </div>
</template>
<script>
    import moment from 'moment';

    export default {
        data (){
            return {}
        },
        emits: ['CHANGE_MONTH'],
        props : {
            currentMonth : {},
        },
        computed: {
            title () {
                let date = this.currentMonth;
                if (!this.currentMonth) return;
                if(date.format('YYYY') === moment().format('YYYY')) {
                    return date.format('MMMM').toUpperCase();
                }
                return date.format('MMMM YYYY').toUpperCase();
            }
        },
        methods : {
            goPrev () {
                let payload = moment(this.currentMonth).subtract(1, 'months').startOf('month');
                this.$emit('CHANGE_MONTH', payload);
            },
            goNext () {
                let payload = moment(this.currentMonth).add(1, 'months').startOf('month');
                this.$emit('CHANGE_MONTH', payload);
            }
        }
    }
</script>
<style>
    .full-calendar-header{
        display: flex;
        align-items: center;
    }
    .header{
        display: flex;
        align-items: center;
    }
    .title {
        text-align: center;
        font-size: 1.5em;
        font-weight: bold;
        min-width: 170px;
        margin: 0 1rem;
    }
    .language-select {
        display: inline-block;
        width: 50%;
    }
</style>