<div class="header">
	<div class="nav-bar">
		<div class="nav-section nav-logo">
			<div><img src="/mf-logo-2.png" alt="mapfeed logo" /></div>
		</div>
	</div>
</div>

<slot />

<div class="site-footer">
	<div>© 2023 MapFeed</div>
	<a href="/about">About</a>
	<a href="/FAQ">FAQ</a>
	<a href="/terms">Terms of Use</a>
	<a href="/privacy">Privacy Policy</a>
	<a href="/cookies">Cookies Policy</a>
	<a href="/disclaimer">Disclaimer</a>
	<a href="/contact">Contact</a>
</div>

<style lang="sass">
    a
        text-decoration: none
        color: inherit

    .site-footer 
        font-size: 12px
        display: flex
        justify-content: space-between
        color: var(--text-secondary)
        background: #fcfcfc
        padding: 9px 36px
        border-top: 1px solid var(--border-color)

    .header 
        position: absolute
        width: 100%
        top: 0
        color: #fabc04

        img
            width: 50px
            height: 50px
</style>
