<template>
    <header class="header sticky">
        <div class="container">
            <div class="left">
                <g-link :to="{ name: 'home' }" class="home-link">
                    <img 
                        src="../../static/logo.svg"
                        :alt="settings.site_name" 
                        class="logo"
                    />
                </g-link>
            </div>
            <nav class="nav right">
                <g-link class="nav__link" to="/blog">Blog</g-link>
                <g-link class="nav__link catalog" :to="{ name: 'home' }">Catálogo</g-link>
            </nav>
        </div>
    </header>
</template>

<script>
export default {
  data() {
    return {
        logo: require("../../static/logo.svg"),
        settings: require("../../data/theme.json")
    }
  }
}
</script>

<style scoped lang="scss">
.header {
    position: relative;
    height: 6rem;
    z-index: 10;
}
.header.sticky {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
}
.header > .container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 100%;
}
.home-link {
    text-decoration: none;
}
.logo {
    height: 3.8rem;
}
@media (max-width: 375px) {
    .logo {
        height: 3.4rem;
    }
}
.site-name {
    font-size: 0.9rem;
    font-weight: 700;
    letter-spacing: 0.05em;
    text-decoration: none;
    text-transform: uppercase;   
}
.nav > * {
    font-size: 0.9rem;
    font-weight: 600;
    text-decoration: none;
    margin-top: 4px;
    margin-right: 3rem;
    padding-bottom: 4px;
    border-bottom: 1px solid;
    border-color: transparent;
    transition: border 0.15s;
}
@media (min-width: 375px) {
    .nav > * {
        margin-right: 1rem;
    }
}
.nav > *:last-of-type {
    margin: 0;
}
.nav > *:hover {
    border-color: inherit;
}
.nav > .active {
    border-color: inherit;
}

.nav {
  &.right {
      .catalog {
        background: linear-gradient(90deg, #EC008C 0%, #FC6767 100%);
        padding: 8px 12px;
        color: white;
        display: inline-block;
        transition: .2s ease;
        border: 0;
        &:hover {
          box-shadow: -8px 8px black;
          transform: translate(4px, -4px);
        }
      }
  }
}
</style>
