<template>
    <div class="day-cell"
         :class="{'today' : day.isToday, 'future' : day.isFuture, 'weekend': day.isWeekEnd, 'selected-day':isDaySelected}"
        @click="showDayOptions">
        <div class="row">
            
            <div class="col-sm-12">
                <p class="day-number">{{ day.date.format('D') }}</p>
            </div>
        </div>
        <div class="event-box">
            <event-card
                    :event="event"
                    :key="event.id"
                    :day-date="day.date"
                    v-for="event in day.events">
            </event-card>
        </div>
    </div>
</template>
<script>
    import EventCard from './EventCard.vue';
    export default {
        components: {
            EventCard
        },
        props:{
            day: {
                type: Object
            },
            firstDay: {
                type: String
            },
        },
        data () {
            return {
                isDaySelected: false
            }
        }
    }
</script>
<style>
    .day-cell {
        flex: 1;
        min-height: 112px;
        width: calc(100% / 7);
        padding: 4px;
        border-right: 1px solid #e0e0e0;
        border-bottom: 1px solid #e0e0e0;
        background: rgba(147, 147, 147, 0.1);
        overflow-x: visible;
        position: relative;
    }
    .day-number {
        text-align: right;
        color: rgba(0, 0, 0, .25);
        font-size: 1em;
        padding: 5px;
    }

    .future {
        background: #fff;
    }

    .future p {
        color: rgba(0, 0, 0, .8);
        font-size: 1.5em;
        font-weight: bold;
    }


    .weekend p {
        color: rgba(122, 10, 117, .7);
    }

    .today {
        border: 2px solid #727171;
        background: #fff;
    }

    .today p {
        font-weight: bold;
        font-size: 1.5em;
        color: #367016 !important;
    }
    
</style>