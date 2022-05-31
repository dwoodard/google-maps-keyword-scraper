<template>
  <div id="results">


    <menu class="menu">

      <button class="menu__item active" style="--bgColorItem: #0075ea;" @click="download">
        <svg class="icon" viewBox="0 0 24 24">
          <path d="M3.8,6.6h16.4"/>
          <path d="M20.2,12.1H3.8"/>
          <path d="M3.8,17.5h16.4"/>
        </svg>
      </button>

      <button class="menu__item" style="--bgColorItem: #f54888;">
        <svg class="icon" viewBox="0 0 24 24">
          <path d="M6.7,4.8h10.7c0.3,0,0.6,0.2,0.7,0.5l2.8,7.3c0,0.1,0,0.2,0,0.3v5.6c0,0.4-0.4,0.8-0.8,0.8H3.8
        C3.4,19.3,3,19,3,18.5v-5.6c0-0.1,0-0.2,0.1-0.3L6,5.3C6.1,5,6.4,4.8,6.7,4.8z"/>
          <path d="M3.4,12.9H8l1.6,2.8h4.9l1.5-2.8h4.6"/>
        </svg>
      </button>


    </menu>


    <section>
      {{ places }}
      {{ searchTitle }}
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
      places: [1, 2, 3]
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
    }
  },
  mounted () {
    console.log('mounted')

    const body = document.body
    const bgColorsBody = ['#ffb457', '#ff96bd', '#9999fb', '#ffe797', '#cffff1']
    const menu = body.querySelector('.menu')
    const menuItems = menu.querySelectorAll('.menu__item')
    // const menuBorder = menu.querySelector('.menu__border')
    let activeItem = menu.querySelector('.active')

    function clickItem (item, index) {
      menu.style.removeProperty('--timeOut')

      if (activeItem === item) return

      if (activeItem) {
        activeItem.classList.remove('active')
      }

      item.classList.add('active')
      body.style.backgroundColor = bgColorsBody[index]
      activeItem = item
      offsetMenuBorder(activeItem, menuBorder)

    }

    function offsetMenuBorder (element, menuBorder) {

      const offsetActiveItem = element.getBoundingClientRect()
      const left = Math.floor(
          offsetActiveItem.left - menu.offsetLeft - (menuBorder.offsetWidth - offsetActiveItem.width) / 2) + 'px'
      menuBorder.style.transform = `translate3d(${left}, 0 , 0)`

    }

    offsetMenuBorder(activeItem, menuBorder)

    menuItems.forEach((item, index) => {

      item.addEventListener('click', () => clickItem(item, index))

    })

    window.addEventListener('resize', () => {
      offsetMenuBorder(activeItem, menuBorder)
      menu.style.setProperty('--timeOut', 'none')
    })

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
  height: 100vh;
  background:#ffffffcf;
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
  transform: translate3d(0, -32px, 0);
  height: 10px;
  width: 60px;
  border-top-left-radius: 30px;
  border-top-right-radius: 30px;
  top: 28px;
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
