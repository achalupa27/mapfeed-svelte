<div class="header">
	<div class="nav-bar">
		<div class="nav-section nav-logo">
			<div><img src="/mf_logo.png" alt="mapfeed logo" /></div>
			<div><a href="/">MapFeed</a></div>
		</div>
		<div class="nav-section nav-details">
			<div class="nav-pricing"><a href="/pricing">Pricing</a></div>
			<div class="nav-pricing"><a href="/pricing">Features</a></div>
		</div>
		<div class="nav-section nav-register">
			<a href="/sign-in"><div class="nav-signin">Sign In</div></a>
			<a href="/sign-up"><div class="nav-signin">Sign Up</div></a>
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

        .nav-bar
            display: flex
            align-items: center
            padding: 12px 32px
            justify-content: space-between

        .nav-section 
            flex: 1
            display: flex
            gap: 24px

        .nav-details
            display: flex
            justify-content: center

        .nav-register
            display: flex
            justify-content: right
            gap: 12px

        .nav-logo
            font-size: 30px
            font-weight: 700
            display: flex
            align-items: center
            gap: 12px

            img
                width: 50px
                height: 50px
</style>
