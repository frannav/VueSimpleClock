<template>
  <div class="clock">
    <div class="hours">{{ hours | toHuman }}</div>
    <div class="sep">:</div>
    <div class="minutes">{{ minutes | toHuman }}</div>
    <div class="sep">:</div>
    <div class="seconds">{{ seconds | toHuman }}</div>
    <div class="mode">{{ mode }}</div>
  </div>
</template>


<script>
export default {
  name: "ComponentClock",
  data() {
    return{
      hours: "--",
      minutes: "--",
      seconds: "--",
      mode: "am"
    }
  },
  methods: {
    tick() {
      const date = new Date();
      this.hours = date.getHours();
      this.minutes = date.getMinutes();
      this.seconds = date.getSeconds();
      this.mode = this.hours >= 12 ? 'pm' : 'am';
    }
  },
  mounted() {
    setInterval(this.tick, 1000);
  },
  filters: {
    //Son como unos metodos pero para utilizar en las plantillas (templates)  
    toHuman(value) {
      return value.toString().padStart(2, '0')
    }
  }
}
</script>




<!-- 
Si queremos tener varios componentes reloj, por ejemplo, habría que renombrar el archivo APP.vue clock.vue, luego cambiar el nombre de app a clock 
Luego creamos el nuevo archivo app.vue

y en la parte de script hacemos
<script>
import clock from /ruta del archivo/
export default {
  name: 'App'
  components: {
    clock
  }
}
-->