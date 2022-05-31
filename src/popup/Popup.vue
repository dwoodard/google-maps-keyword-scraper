<template>
  <div id="popup">

    <div class="popup-content">
      <p>Google Map Scraper</p>
      {{ places }}
    </div>


  </div>
</template>

<script lang="ts">
import {defineComponent} from 'vue'

export default defineComponent({
  name: 'Popup',
  data() {
    return {

    }
  },
  setup() {
    return {}
  },
  mounted() {},
  methods: {},
})

</script>

<style scoped>
.popup-content {

  background-color: #fafafa;
  width: 500px;
  height: 500px;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0px 0px 5px 0px rgba(0,0,0,0.75);
}
</style>
