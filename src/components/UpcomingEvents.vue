<template>
	<div class="containter">
		<div class="event-menu">
			<button class="button">Save</button>
		</div>
		<div class="event-list">
			<div class="event-item" v-for="event in events">
				<div class="event-item__icon"></div>
				<div class="event-item__title">{{event.title}}</div>
				<div class="event-item__day">{{event.date.getDay()}}</div>
			</div>
		</div>
	</div>
</template>

<script>
	let demoData = [
		{title: 'Модель формы 56', date: new Date(2019, 12, 7)},
		{title: 'Слайдер', date: new Date(2019, 12, 5)},
		{title: 'Макет 19265', date: new Date(2019, 12, 3)},
	]
	export default{
		data(){
			return{
				events: demoData,
			}
		},
		methods:{
			save(){

			}
		}
	}
</script>

<style lang="stylus" scoped>
	@import '../smart-grid.styl'
	color0 = #252C3C
	color1 = #2a3950 
	color2 = #c1bdbd
	.button
		height 30px
		background-color #275AA7
		padding-right 10px
		padding-left 10px
		border solid 1px color0 
		border-radius 3px
		opacity 0.7
		color color2 
		&:hover
			opacity 1

	.containter
		color #c1bdbd
		font-size 0.9em
		font-family 'Arial'
		font-weight 300
		letter-spacing 0.05em
	.event-menu
		row-flex()
		justify-content center
		align-items center
		height 60px
		margin-bottom 10px
		background-color color1 
	
	.event-item
		row-flex()
		align-items center
		margin-bottom 2px
		height 34px
		background-color color1
		&:hover
			background-color #485F8D
		&__icon
			text-align center
			col-padding()
			size(2)
		&__title
			col-padding()
			size(7)
		&__day
			text-align center
			col-padding()
			size(3)
</style>