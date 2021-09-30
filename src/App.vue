<template>
    <div id="app">
        <div class="container">
            <h1>Calendar vue</h1>
            <app-calendar
                    :first-day="1"
                    :all-events="events"
            ></app-calendar>
        </div>
    </div>
</template>

<script>
	import AppCalendar from './AppCalendar.vue';
    export default {
		components: {
            AppCalendar
        },
        data() {
            return {
                events: [ 
                    {
                        id:1,
                        title:'14:00 Lorem ipsum dolor',
                        type: 'panel-danger',
                        date: new Date()
                    },
                    {
                        id:2,
                        title:'17:00 sit amet consectetur adipisicing elit. Cum beatae',
                        type: 'panel-success',
                        date: new Date()
                    },
                    {
                        id:3,
                        title:'10:30 ipsum dolor sit amet consectetur adipisicing elit',
                        type: 'panel-primary',
                        date: new Date(new Date().setHours(new Date().getHours() + 2*24)) // add 2 days
                    },
                    {
                        id:4,
                        title:'12:00 Cum beatae ea delectus enim mollitia suscipit, quo distinctio aut dolorum',
                        type: 'panel-success',
                        date: new Date(new Date().setHours(new Date().getHours() + 5*24)) // add 5 days
                    },
                ]
            }
        },
        
    }
</script>
