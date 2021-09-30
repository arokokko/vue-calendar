<template>
    <div id="app">
        <div class="container">
            <h1>Calendar vue</h1>
            <app-calendar
                    :first-day="1"
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
        
        
    }
</script>
