<template>
  <transition name="fade" appear>
   
  
    <!-- <div class="screen"> -->
    <div class="screen banner">

      <header class="header">
        <!-- <g-link class="banner-top" to="/ambassador-program">
          <div class="layout__content">We launched Ambassador Program, join!</div>
        </g-link> -->

        <div class="header-content">
          <div class="header-logo">
            <g-link to="/">
              <g-image :alt="$static.metadata.siteName + ' logotype'" src="~/assets/images/robonomics-logo.svg"/>
              <span class="logo-text">Robonomics Network</span>
            </g-link>
          </div>

          <div class="header-side">
            <HeaderNav/>
            <ThemeSwitcher/>
            <languageSwitcher/>

          </div>

          
        </div>
      </header>

      <div class="screen-content">
        
        <slot/>
        <ClientOnly> <Footer/> </ClientOnly>
      </div>

      <div class="sidetext sidetext-left">
        <g-link to="/timeline">Founded in 2015</g-link> &nbsp; &bull; &nbsp; 
        <g-link :to="this.releaseLink">Latest release {{ this.releaseTime }}</g-link>
      </div>

    </div>
  
  </transition>
</template>


<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>


<style scoped>

  .banner-top {
    position: relative;
    height: var(--space-bannertop);
    display: flex;
    justify-content: center;
    align-items: center;

    padding-right: var(--screen-padding-right);
    padding-left: var(--screen-padding-right);

    text-decoration: none;
    overflow: hidden;

    background-color: var(--color-blue);
    background-image: url(/ambassador-pattern.jpg);
    background-position: 0 50%;
    background-repeat: repeat-x;
    /* background-color: var(--color-red); */
    color: #fff !important;
    font-weight: bold;
    text-transform: uppercase;
    letter-spacing: 1px;
    /* font-size: 90%; */
    line-height: 1;

    font-family: var(--font-family-code);
    text-shadow: 1px 1px 0 #000;

    /* background-image: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 40 40">\
			<text x="20" y="20" font-size="10" style="fill:#ccc">🤖</text>\
			</svg>');
			background-size: 30px 30px; */
  }

  .header-logo {
    padding-left: calc(var(--screen-padding-left) - 9px);
    /* max-width: 283px;
    width: 100%; */
    /* width: calc( var(--screen-padding-left) - calc(var(--logo-padding)*1.5)); */
    background-color: var(--body-bg);
  }

  .header-logo a {
    width: 100%;
    display: flex;
    align-items: center;
    text-decoration: none;
  }

  .header-logo a {
    color: currentColor;
  }

  .header-logo a img {
    margin-right: 20px;
  }


  .dark-theme .header-logo a img {
    filter:  grayscale(1) invert(1);
  }

  .logo-text {
    font-size: 1rem;
    white-space: nowrap;
    text-transform: uppercase;
    color: var(--color-dark);
  }

  @media screen and (max-width: 950px) {
    .header-logo  {
      margin-top: 6px;
      width: 40%;
    }

    .header-logo a svg {
      width: 100%;
    }

    .header-logo {
      max-width: 100px;
      width: 34%;
      padding-left: 40px;
    }

    .logo-text {
      display: none;
      font-size: 0.6rem;
    }
  }

  @media screen and (min-width: 700px) {
    .banner-top {
      font-size: 150%;
    }
  }

  .banner-top:after {
    content: "";
    background: rgba(0, 0, 0, 0.4);
    position: absolute;
    z-index: 0;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }

  .banner-top > div {
    position: relative;
    z-index: 1;
  }


  .header {
    --logo-padding: 0.6rem;

    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index:1000;

    background-color: var(--body-bg);
  }

  /* .header-logo a, .header-logo img { display: block; } */
  
  .header-content {
    display: flex;
    justify-content: space-between;
    align-items: center;

    height: var(--screen-padding-top);
    padding: 2rem ;
    padding-left: var(--logo-padding);
    padding-right: var(--screen-padding-right);
  }

  .sidetext {
    font-family: var(--font-family-code);
    font-size: calc(var(--base-font-size) * 0.8);
    text-transform: uppercase;
  }

  @media screen and (max-width: 660px) {
    .header-logo  {
      /* margin-top: 0; */
      width: 100%;
    }
  }
  
  @media screen and (max-width: 480px) {
    .header-logo  {
      /* margin-top: 0; */
      width: 100%;
      margin-right: 5px;
    }
  }

  @media screen and (max-width: 350px) {
      .sidetext { font-size: 70%; }
    }

  .sidetext a:not(.button) {
    color: var(--text-color);
    text-decoration: none;
  }

  .sidetext-left {
    position:  fixed;
    left: calc(var(--screen-padding-left)/4);
    bottom: calc(var(--screen-padding-bottom)/1.8);

    transform: rotate(-90deg);
    transform-origin: 0 0;
    white-space: nowrap;
  }

  .sidetext-left.active--exact, .sidetext-left a.active--exact { opacity: .5; }


.screen {
	position: relative;
  background-color: var(--color-gray-light);
  border-style: solid;
  border-color: var(--body-bg);
  border-width: 0 var(--screen-padding-right) 0 var(--screen-padding-left);
  padding-top: var(--screen-padding-top);
  padding-bottom: var(--screen-padding-bottom);
  height: 100vh;
  scrollbar-width: none;
}


	.screen::-webkit-scrollbar { display: none; }


  .screen:after {
    content: "";
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    height: var(--screen-padding-bottom);
    background: var(--color-light);
    z-index: 1000;
  }


.screen-content {
  background-color: var(--color-gray-light);
}

/* .screen:not(.banner) {
 padding-top: calc(var(--screen-padding-top) + var(--space-bannertop));
} */

.header-side {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header-side > *:not(:last-child) {
      margin-right: var(--space);
    }

</style>


<script>

import axios from 'axios'
import moment from 'moment'

export default {

  components: {
    Footer: () => import('~/components/Footer.vue'),
    languageSwitcher: () => import('~/components/languageSwitcher.vue'),
    ThemeSwitcher: () => import('~/components/ThemeSwitcher.vue'),
    HeaderNav: () => import('~/components/HeaderNav.vue'),
  },
  data () {
    return {
      release: null,
      update: null,
      releaseTime: null,
      releaseLink: null
    }
  },
  methods: {
    BannerLink(p) {
      let current = this.$router.currentRoute.path
      // current = current.replace(/\/$/,'')
      // return current != p
      return current.includes(p)
    }
  },
  async mounted () {
      try {
        const results = await axios.get(
          'https://api.github.com/repos/airalab/robonomics/releases/latest'
        )

        this.release = results.data;
        this.update = this.release['published_at'];
        this.releaseTime = moment(this.update).from();
        this.releaseLink = this.release['html_url'];

      } catch (error) {
        console.log(error)
      }
    }
}
</script>
