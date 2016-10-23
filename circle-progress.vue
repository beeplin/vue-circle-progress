<template>
  <div class="v-circle" :style="circleStyle">
    <div class="mask full" :style="[maskStyle, transitionStyle, rotateStyle]">
      <div class="fill" :style="[fillStyle, transitionStyle, rotateStyle]"></div>
    </div>
    <div class="mask half" :style="[maskStyle]">
      <div class="fill" :style="[fillStyle, transitionStyle, rotateStyle]"></div>
      <div class="fill fix" :style="[fillStyle, fixStyle, transitionStyle]"></div>
    </div>
    <div class="pv" :style="pvStyle">
      <span class="progress" :style="progressTextStyle">
      {{ pv || 0 }}
    </span>
    </div>
  </div>
</template>
<script lang="coffee">

DEFAULT_WIDTH = 150
DEFAULT_BOLD = 5
DEFAULT_FONT_SIZE = 64
DEFAULT_BORDER_COLOR = '#bdc3c7'
DEFAULT_TEXT_COLOR = '#bdc3c7'
DEFAULT_FILL_COLOR = '#2ecc71'
DEFAUTL_BG_COLOR = '#f9f9f9'
DEFAUTL_TEXT_BG_COLOR = '#333333'

export default v =

  name: "circle"

  props: [
    'color'
    'width'
    'fontSize'
    'pv'
    'textColor'
    'bold'
    'textBgColor'
    'borderColor'
    'during'
    'bgColor'
  ]

  methods:

    setClip: (t, r, b, l) ->
      "rect(#{t}px, #{r}px, #{b}px, #{l}px)"

    setTransformStyle: (pv, type) ->
      deg = Math.floor(pv / 100 * 180)
      if type == 'fix'
        # remove the gap between two half circles
        return "rotate(#{deg * 2}deg)"
      "rotate(#{deg}deg)"

    setTransitionStyle: (t) ->
      "transform #{t}s"

  computed:
    transformStyleValue: -> @setTransformStyle(@pv)
    innerCircleWidth: -> (@width or DEFAULT_WIDTH) - (2 * (@bold or DEFAULT_BOLD)) + 'px'
    fixTransformStyleValue: -> @setTransformStyle(@pv, 'fix')
    transitionStyleValue: -> @setTransitionStyle(@during or 0.8)
    circleStyle: ->
      borderColor: @borderColor or DEFAULT_BORDER_COLOR
      borderStyle: 'solid'
      borderWidth: DEFAULT_BOLD + 'px'
      width: (@width or DEFAULT_WIDTH) + 'px'
      height: (@width or DEFAULT_WIDTH) + 'px'
      backgroundColor: @bgColor or DEFAUTL_BG_COLOR
    progressTextStyle: ->
      fontSize: (@fontSize or DEFAULT_FONT_SIZE) + 'px'
      color: @textColor or DEFAULT_TEXT_COLOR
    fillStyle: ->
      backgroundColor: @color or DEFAULT_FILL_COLOR
      width: (@width or DEFAULT_WIDTH) + 'px'
      height: (@width or DEFAULT_WIDTH) + 'px'
      clip: @setClip(0, @width / 2, @width, 0)
    rotateStyle: ->
      transform: @transformStyleValue
      webkitTransform: @transformStyleValue
      msTransform: @transformStyleValue
      oTransform: @transformStyleValue
      mozTransform: @transformStyleValue
    transitionStyle: ->
      transition: @transitionStyleValue
      webkitTransition: @transitionStyleValue
      mozTransition: @transitionStyleValue
      oTransition: @transitionStyleValue
      msTransition: @transitionStyleValue
    maskStyle: ->
      width: (@width or DEFAULT_WIDTH) + 'px'
      height: (@width or DEFAULT_WIDTH) + 'px'
      clip: @setClip(0, @width, @width, @width / 2)
    pvStyle: ->
      backgroundColor: @textBgColor or DEFAUTL_TEXT_BG_COLOR
      width: @innerCircleWidth
      height: @innerCircleWidth
      lineHeight: @innerCircleWidth
    fixStyle: ->
      transform: @fixTransformStyleValue
      webkitTransform: @fixTransformStyleValue
      mozTransform: @fixTransformStyleValue
      oTransform: @fixTransformStyleValue
      msTransform: @fixTransformStyleValue

</script>
<style scoped>
  .v-circle {
    border-radius: 50%;
    position: relative;
  }

  .v-circle .mask,
  .v-circle .fill {
    position: absolute;
    border-radius: 50%;
    backface-visibility: hidden;
  }

  .v-circle .pv {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    margin: auto;
    z-index: 1;
    border-radius: 50%;
    text-align: center;
  }

  .v-circle .progress {
    margin: 0;
    padding: 0;
    font-family: 'Impact';
  }

</style>
