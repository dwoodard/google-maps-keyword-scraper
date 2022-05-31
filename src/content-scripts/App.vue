<template>
  <div id="results">


    <menu class="menu" @click="clickItems($event)">

      <button class="menu__item active" style="--bgColorItem: #0075ea;" @click="download">
        <svg class="icon" viewBox="0 0 24 24">
          <path d="M3.8,6.6h16.4"/>
          <path d="M20.2,12.1H3.8"/>
          <path d="M3.8,17.5h16.4"/>
        </svg>
      </button>

      <button class="menu__item" style="--bgColorItem: #f58a48;">
        <svg class="icon" viewBox="0 0 24 24">
          <path d="M6.7,4.8h10.7c0.3,0,0.6,0.2,0.7,0.5l2.8,7.3c0,0.1,0,0.2,0,0.3v5.6c0,0.4-0.4,0.8-0.8,0.8H3.8
        C3.4,19.3,3,19,3,18.5v-5.6c0-0.1,0-0.2,0.1-0.3L6,5.3C6.1,5,6.4,4.8,6.7,4.8z"/>
          <path d="M3.4,12.9H8l1.6,2.8h4.9l1.5-2.8h4.6"/>
        </svg>
      </button>


    </menu>


    <section>
      {{ places }}
    </section>


  </div>
</template>

<script lang="js">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'App',
  data () {
    return {
      searchTitle: document.querySelector('#searchboxinput')?.value | undefined,
      places: null,
      activeItem: document.querySelector('.active'),
      searchResults: null
    }
  },
  setup () {
    return {}
  },
  methods: {
    download () {
      console.log('download json')
    },
    menu () {
      console.log('menu')
    },

    checkPlaces () {
      const element = document.querySelector('[aria-label~=Results]')

      //run function every second stop after 10 seconds
      let scrollInterval = setInterval(() => {
        element.scroll({ top: element.scrollHeight, behavior: 'smooth' });
        console.log('scroll height', element.scrollHeight)
      }, 500)

      setTimeout(() => {
        clearInterval(scrollInterval)

        this.places =  [this.places, ...document.querySelectorAll('.fontHeadlineSmall')]
        document.querySelector('.punXpd>button+button').click()
        this.checkPlaces()
      }, 6000)
    },
    clickItems (event) {

      this.activeItem = event.target

      //loop through all menu items
      const menuItems = document.querySelectorAll('.menu__item')

      //remove active class for all menu items
      menuItems.forEach((item) => {
        // remove active class on all menu items
        item.classList.remove('active')

        // add active class on the clicked menu item
        if (item === event.target.closest('.menu__item')) {
          item.classList.add('active')
        }
      })




      // document.querySelector('#results').style.backgroundColor = bgColorsBody[index]
    }
  },
  mounted () {
    console.log('mounted');

    this.checkPlaces()



    console.log(this.places);

  }
})
</script>

<style>
#results {

}

html {

  box-sizing: border-box;
  --bgColorMenu: #000000aa;
  --duration: .7s;

}

html *,
html *::before,
html *::after {
  box-sizing: inherit;
}


#results {
  margin: 0;
  height: 100vh;
  overflow: hidden;
  align-items: center;
  justify-content: center;
  z-index: 9999;
  position: fixed;
  top: 0;
  left: calc(100% - 32em);
  right: 0;
  bottom: 0;
}

#results > section {
  overflow: auto;
  height: 100vh;
  background: #ffffffcf;
}

.menu {
  background: #000000e8;
  margin: 10px 0 0;
  display: flex;
  padding: 0 2.85em;
  position: relative;
  align-items: center;
  justify-content: center;

}

.menu__item {

  all: unset;
  flex-grow: 1;
  z-index: 100;
  display: flex;
  cursor: pointer;
  position: relative;
  border-radius: 50%;
  align-items: center;
  will-change: transform;
  justify-content: center;
  padding: 0.55em 0 0.85em;
  transition: transform var(--timeOut, var(--duration));

}

.menu__item::before {

  content: "";
  z-index: -1;
  width: 4.2em;
  height: 4.2em;
  border-radius: 50%;
  position: absolute;
  transform: scale(0);
  transition: background-color var(--duration), transform var(--duration);

}


.menu__item.active {
  /*transform: translate3d(0, -32px, 0);*/
  /*height: 10px;*/
  /*width: 60px;*/
  /*border-top-left-radius: 30px;*/
  /*border-top-right-radius: 30px;*/
  /*top: 28px;*/
}

.menu__item.active::before {

  transform: scale(1);
  background-color: var(--bgColorItem);

}

.icon {

  width: 2.6em;
  height: 2.6em;
  stroke: white;
  fill: transparent;
  stroke-width: 1pt;
  stroke-miterlimit: 10;
  stroke-linecap: round;
  stroke-linejoin: round;
  stroke-dasharray: 400;

}

.menu__item.active .icon {

  animation: strok 1.5s reverse;

}

@keyframes strok {
  100% {
    stroke-dashoffset: 400;
  }
}

.menu__border {
  left: 0;
  bottom: 99%;
  width: 10.9em;
  height: 2.4em;
  position: absolute;
  clip-path: url(#menu);
  will-change: transform;
  background-color: var(--bgColorMenu);
  transition: transform var(--timeOut, var(--duration));

}

.svg-container {

  width: 0;
  height: 0;
}


@media screen and (max-width: 50em) {
  .menu {
    font-size: .8em;
  }
}
</style>
