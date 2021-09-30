<template>
    <div class="row">

        <div class="panel panel-default">

            <div class="panel-body">
                <div class="row">
                    <div class="col-sm-12">
                        <header-calendar :current-month="currentMonth"
                                         :first-day="firstDay"
										@CHANGE_MONTH="changeMonth($event)"
                        >
                        </header-calendar>

                        <div class="full-calendar-body">
                            <div class="weeks">
                                <strong class="week" v-for="dayIndex in 7" :key="dayIndex + 'week'">{{ weekDayName((dayIndex - 1), firstDay) }}</strong>
                            </div>

                            <div class="dates" ref="dates">
                                <week-calendar v-for="(week, index) in Weeks"
                                      :firstDay="firstDay"
                                      :key="index"
                                      :week="week">
                                </week-calendar>
                            </div>
                        </div> 
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
	import moment from 'moment';
    import HeaderCalendar from './components/Header.vue';

	export default {
        components: {
			HeaderCalendar,
		},
		data () {
			return {
				currentMonth: moment().locale('ru').startOf('month'),
			}
		},
		props: {
			
			firstDay: {
				type: Number || String,
				validator (val) {
					let res = parseInt(val);
					return res >= 0 && res <= 6
				},
				default: 0
			}
		},
		
		
		methods: {
			
			changeMonth(e) {
				this.currentMonth = e.locale('ru').startOf('month');
			},
			
		},
		
	}

</script>
<style>
    ul, p {
        margin: 0;
        padding: 0;
    }

    .full-calendar-body {
        margin-top: 20px;
    }
    .weeks {
        display: flex;
        border-top: 1px solid #e0e0e0;
        border-bottom: 1px solid #e0e0e0;
        border-left: 1px solid #e0e0e0;
    }
    .week {
        flex: 1;
        padding: 5px;
        text-align: center;
        border-right: 1px solid #e0e0e0;
    }

    .dates {
        position: relative;
    }
</style>