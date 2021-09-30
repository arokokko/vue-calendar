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
	import WeekCalendar from './components/Week.vue';

	export default {
        components: {
			HeaderCalendar,
			WeekCalendar
		},
		data () {
			return {
				currentMonth: moment().locale('ru').startOf('month'),
			}
		},
		props: {
			allEvents: {
				type: Array,
				default: function () {
					return [];
				}
			},
			firstDay: {
				type: Number || String,
				validator (val) {
					let res = parseInt(val);
					return res >= 0 && res <= 6
				},
				default: 0
			}
		},
		
		computed: {
			Weeks () {
				let monthMomentObject = this.getMonthViewStartDate(this.currentMonth, this.firstDay);
				let weeks = [], week = [];

				let daysInCurrentMonth = this.currentMonth.daysInMonth();

				for ( let weekIndex=0; weekIndex < 5; weekIndex++) {

					week = [];
					for (let dayIndex=0; dayIndex < 7; dayIndex++) {

						week.push(this.getDayObject(monthMomentObject, dayIndex));

						monthMomentObject.add(1, 'day');
					}

					weeks.push(week);
				}

				let diff = daysInCurrentMonth-weeks[4][6].date.format('D');


				if(diff > 0 && diff < 3){
					week = [];
					for (let dayIndex=0; dayIndex < 7; dayIndex++) {

						week.push(this.getDayObject(monthMomentObject, dayIndex));

						monthMomentObject.add(1, 'day');
					}

					weeks.push(week);
				}

				return weeks;
			},
			events: function () {
				return this.allEvents;
			}
		},
		methods: {
			getEvents (date) {
				return this.events.filter(event => {
					return date.isSame(event.date, 'day') ? event : null;
				});
			},

			getMonthViewStartDate (date, firstDay) {
				firstDay = parseInt(firstDay);

				let start = moment(date);
				let startOfMonth = moment(start.startOf('month'));

				start.subtract(startOfMonth.day(), 'days');

				if (startOfMonth.day() < firstDay) {
					start.subtract(7, 'days');
				}

				start.add(firstDay, 'days');

				return start;
			},

			getDayObject(monthMomentObject, dayIndex){
				return {
					isToday: monthMomentObject.isSame(moment(), 'day'),
					isFuture: monthMomentObject.isAfter(),
					weekDay: dayIndex,
					isWeekEnd: (dayIndex == 5 || dayIndex == 6),
					date: moment(monthMomentObject),
					events: this.getEvents(monthMomentObject)
				};
			},
			changeMonth(e) {
				this.currentMonth = e.locale('ru').startOf('month');
			},
			weekDayName (weekday, firstDay) {
				firstDay = parseInt(firstDay);
				const localMoment = moment().locale('ru');
				return localMoment.localeData().weekdays()[(weekday + firstDay) % 7].toUpperCase();
			}
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