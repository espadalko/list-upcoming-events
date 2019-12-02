<template>
	<div class="containter">
		<div class="menu">

			<input @keyup.enter="add()" v-model="input" type="text" class="form" autofocus>

		</div>
		<div class="list">
			<div class="item" :class="{muted: item.term < 0}" :style="{order: item.term}" v-for="(item, index) in filter">
				<div class="item__day">{{ item.term }}</div>
				<div class="item__title">{{ item.title }}</div>
				<div @click="remove(index)" class="item__remove"> X </div>
			</div>
		</div>
	</div>
</template>

<script>
	// рассчитать оставшееся количество дней
	let demoData = [
		{id: 0, title: 'Модель формы 56', date: new Date(2019, 12, 7), term: 0},
		{id: 1, title: 'Слайдер', date: new Date(2019, 12, 5), term: 0},
		{id: 2, title: 'Макет 19265', date: new Date(2019, 12, 2), term: 0},
	]

	export default{
		name: 'UpcomingEvents',
		data(){
			return{
				items: demoData,
				newDate: new Date().getDate(),
				input: ''
			}
		},
		mounted(){
			this.loadingLocalData()
		},
		methods:{
			term(index){
				// @@@
				// return  this.items[index].date.getDate() - this.newDate.getDate() 
			},
			add(){
				// parse input
				let re = /(^[0-9]+)[ ]?/
				let title = this.input.replace(re, '') 
				let day = parseInt((this.input.match(re) || [0,0])[1]) 
				// let dayT = this.input.match(re)[1] 
				// console.log(dayT)
				// let day = 1
				let date = new Date()
				date.setDate(date.getDate() + day)
				let obj = {
					title: title, 
					date: date 
				} 
				// add
				this.items.push(obj)
				this.input = ''
				this.saveLocalData()
			},
			loadingLocalData(){
				let local = localStorage.getItem('local')
				local = local ? JSON.parse(local) : [] 
				local.forEach( e => {
					e.date = new Date(e.date)
				})
				this.items = local 
			},
			saveLocalData(){
				localStorage.setItem('local', JSON.stringify(this.items))
			},
			remove(index){
				this.items.splice(index, 1)
				this.saveLocalData()
			}
		},
		computed:{
			filter(){
				this.items.forEach((element, index) => {
					element.term = element.date.getDate() - this.newDate
				})
				return this.items
			}
		}
	}
</script>

<style lang="stylus" scoped>
	@import '../smart-grid.styl'
	color0 = #252C3C
	color1 = #2a3950 
	color2 = #c1bdbd
	input
		height 100% 
		width 100% 
		outline none
		// background-color transparent 
		// background-color color1
		border 0px 
		opacity 0.5
		background-color color1
		padding 0 15px
		font-size 1.1em
		color color1
		&:focus
			background-color color2
		
	.button
		height 30px
		background-color #275AA7
		margin-right 2px
		margin-left 2px
		padding-right 10px
		padding-left 10px
		border solid 1px color0 
		border-radius 3px
		opacity 0.7
		color color2 
		&:hover
			opacity 1
	.muted
		opacity 0.4
	.containter
		color #c1bdbd
		font-size 0.9em
		font-family 'Arial'
		font-weight 300
		letter-spacing 0.05em
	.menu
		row-flex()
		justify-content center
		align-items center
		height 60px
		margin-bottom 10px
		// background-color color1
		// border-radius 3px
		// opacity 0.5
	.list
		display flex
		flex-direction column
	.item
		row-flex()
		align-items center
		margin-bottom 2px
		padding-top 10px
		padding-bottom @padding-top
		min-height 34px
		background-color color1
		&:hover
			background-color #485F8D
		&__remove
			col()
			// col-padding()
			size(2)
			// background-color red
			color color0 
			cursor pointer
			text-align center
		&__title
			col()
			// col-padding()
			size(8)
			// background-color green
		&__day
			col()
			// col-padding()
			size(2)
			text-align center
			// background-color blue
</style>