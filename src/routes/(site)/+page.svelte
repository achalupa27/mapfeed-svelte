<div class="home">
	<div class="container">
		<a href="/app"><div class="get-started">Start Exploring</div></a>
	</div>
</div>

<style lang="sass">
	a
		text-decoration: none
		
	.home
		height: 100%
		background-image: url("/map-home-2.png")
		-webkit-background-size: cover
		-moz-background-size: cover
		-o-background-size: cover
		background-size: cover
		display: flex
		justify-content: space-around
		align-items: end
		
	.get-started
		color: rgb(214,184,115)
		color: linear-gradient(309deg, rgba(214,184,115,1) 0%, rgba(198,166,97,1) 72%, rgba(247,232,193,1) 100%)
		border: 2px solid
		height: 42px
		width: 200px
		display: flex
		justify-content: center
		align-items: center
		border-radius: 4px
		font-weight: 700
		margin-top: 20px
		cursor: pointer
		transition: background-color 0.5s ease
		margin-bottom: 80px

		&:hover
			background: rgb(214,184,115)
			background: linear-gradient(309deg, rgba(214,184,115,1) 0%, rgba(198,166,97,1) 72%, rgba(247,232,193,1) 100%)
			color: #0e151d
			border-color: rgb(214,184,115)
			border-color: linear-gradient(309deg, rgba(214,184,115,1) 0%, rgba(198,166,97,1) 72%, rgba(247,232,193,1) 100%)
		
		i
			margin-right: 6px

	.map-img img
		height: 100vh
		width: 100vw

</style>
