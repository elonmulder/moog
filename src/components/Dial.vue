<template>
  <div>
    <button class="dial"v-bind:style="[cssRotate]" v-on:mousedown="onMouseDown"></button>
    Min: {{min}}
    Max: {{max}}
    Value: {{degree}}
  </div>
</template>

<script>
const MAX_ANGLE = 270;

export default {
  name: 'Dial',

  props: {
    max: {
      default: 10,
      required: false
    },

    min: {
      default: 0,
      required: false
    },

    value: {
      default: 0,
      required: false
    }
  },

  data() {
    return {
      handleX: null,
      handleY: null,
      isDragging: false,
      lastAngle: 0,
      mouseX: null,
      mouseY: null,
      originX: null,
      originY: null
    };
  },

  computed: {
    angle() {
      let angle = 0;

      angle = Math.atan2(this.mouseY - 10, this.mouseX - 10);
      this.lastAngle = this.lastAngle =+ angle;

      return angle;
    },

    cssRotate() {
      const style = {};
      const degree = `rotate(${this.degree}deg)`;

      style.transform = degree;

      return style;
    },

    degree() {
      let degree = 0;

      degree = (this.angle * (180 / Math.PI) * -1) + 90;

      return degree;
    }
  },

  methods: {
    onMouseDown(e) {
      const {
        offsetX,
        offsetY,
        pageX,
        pageY
      } = e;

      this.isDragging = true;
    },

    onMouseMove(e) {
      if (this.isDragging) {
        const {
          pageX,
          pageY
        } = e;

        this.mouseX = pageX;
        this.mouseY = pageY;
      }
    },

    onMouseUp() {
      this.isDragging = false;
    }
  },

  mounted() {
    document.onmousemove = this.onMouseMove;
    document.onmouseup = this.onMouseUp;
  }
};
</script>

<style lang="scss">
$SIZE: 100px;

.dial {
  border: 0;
  border-radius: $SIZE / 2;
  height: $SIZE;
  position: relative;
  transform-origin: center;
  width: $SIZE;

  &:before {
    content: '';
    background-color: black;
    display: block;
    height: $SIZE / 2;
    position: absolute;
    right: 50%;
    top: 0;
    transform: translate(-50%, 0);
    width: 2px;
  }
}
</style>
