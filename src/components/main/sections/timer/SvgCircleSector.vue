<template>
  <div>
    <svg class="timer" width="200" height="200"
         xmlns="http://www.w3.org/2000/svg">
      <circle class="
bigCircle
" r="100" cx="100"
              cy="100"></circle>
      <circle class="
smallCircle
" r="90" cx="100"
              cy="100"></circle>
      <text
        v-if="text != ''"
        class="text" x="100" y="100">
        {{text}}
      </text>
      <path class="segment"
            :d="path"
      ></path>
    </svg>
  </div>
</template>
<script>
export default {
  props: ['angle', 'text'],
  computed: {
    path () {
      return calcPath(this.angle)
    }
  }
}
function calcEndPoint (angle) {
  let x, y
  x = 100 - 100 * Math.sin(Math.PI * angle / 180)
  y = 100 - 100 * Math.cos(Math.PI * angle / 180)
  return {
    x, y
  }
}
function calcPath (angle) {
  let d
  let {x, y} = calcEndPoint(angle)
  if (angle <= 180) {
    d = `M100,100 L100, 0 A100,100 0 0,0 ${x}, ${y} z`
  } else {
    d = `M100,100 L100, 0 A100,100 0 0,0 100, 200 A100,100 0 0,
0 ${x}, ${y} z`
  }
  return d
}
</script>
<style scoped lang="scss">
$big-circle-color: gray;
$small-circle-color: lightgray;
$segment-color: darkgray;
$text-color: black;
.bigCircle {
  fill: $big-circle-color;
}
.smallCircle {
  fill: $small-circle-color;
}
.segment {
  fill: $segment-color;opacity: 0.6;
}
.text {
  font-size: 1em;
  stroke-width: 0;
  opacity: .9;
  fill: $text-color;
}
</style>
