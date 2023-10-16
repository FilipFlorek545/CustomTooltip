<script setup>
import {computed, onMounted, ref} from "vue";

  const props = defineProps({
    contents: String,
    position: String,
    customPosition: Array,
    color: String,
    background: String,
    border: String,
    borderRadius: String,
  })
  const showTooltip = ref(false);
  const tooltipWidth = ref('200px');
  const targetElement = ref(null);
  const targetElementPosition = ref(['0','0']);
  const tooltipStyling = ref(['#fff', '#2f2f2f', 'none', '10px'])

  props.color ? tooltipStyling.value[0] = props.color : ''
  props.background ? tooltipStyling.value[1] = props.background : ''
  props.border ? tooltipStyling.value[2] = props.border : ''
  props.borderRadius ? tooltipStyling.value[3] = props.borderRadius : ''

  if(props.contents.split('').length < 16){
    tooltipWidth.value = '140px'
  }
const wrapFunction = (val) => {
  showTooltip.value = val
}

onMounted(() => {
  let targetTooltip = targetElement.value;
  let target = targetElement.value.previousElementSibling;

  [targetTooltip, target].forEach(element => {
    element.addEventListener('mouseover', () => wrapFunction(true));
    element.addEventListener('mouseout', () => wrapFunction(false));
  });

  let tHeight = target.offsetHeight;
  let tWidth = target.offsetWidth;
  let tipHeight = targetTooltip.offsetHeight;
  let tipWidth = targetTooltip.offsetWidth;

  const positionMethods = {
    down: () => [tHeight, (tWidth - tipWidth) / 2],
    top: () => [-tipHeight + 1, (tWidth - tipWidth) / 2],
    left: () => [(tHeight - tipHeight) / 2, -tipWidth],
    right: () => [(tHeight - tipHeight) / 2, tWidth],
    rightDown: () => [tHeight - tipHeight, tWidth],
    rightTop: () => [0, tWidth],
    leftDown: () => [tHeight - tipHeight, -tipWidth],
    leftTop: () => [0 , -tipWidth],
    topRight: () => [-tipHeight, tWidth - tipWidth],
    topLeft: () => [-tipHeight, 0],
    downRight: () => [tHeight, tWidth - tipWidth],
    downLeft: () => [tHeight, 0],
  }

  if(props.position) {
    if(props.position === 'custom'){
      //Give the tooltip its specified position
      targetElementPosition.value = props.customPosition
    }
    else{
      targetElementPosition.value = positionMethods[props.position]()
    }
  }
  else{
    //CALCULATE THE POSITION
    let bDimensions = document.body.getBoundingClientRect()
    let tPosition = target.getBoundingClientRect()

    if(tPosition.x < bDimensions.width / 2 && tPosition.y < bDimensions.height/2){
      targetElementPosition.value = positionMethods.rightDown()
    }
    else if(tPosition.x > bDimensions.width / 2 && tPosition.y < bDimensions.height/2){
      targetElementPosition.value = positionMethods.leftDown()
    }
    else if(tPosition.x < bDimensions.width / 2 && tPosition.y > bDimensions.height/2){
      targetElementPosition.value = positionMethods.rightTop()
    }
    else{
      targetElementPosition.value = positionMethods.leftTop()
    }
  }

})
</script>

<template>
  <div style="display: flex; justify-content: center">
    <div style="position: relative">
    <slot></slot>
      <div ref="targetElement" class="tooltipWrapper"
           :class="{'visible' : showTooltip, 'pointerEventsDisabled' : !showTooltip}">
        <div id="tooltip">
          <span>{{props.contents}}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.tooltipWrapper{
  position: absolute;
  opacity: 0;
  top: v-bind(targetElementPosition[0] + 'px');
  left: v-bind(targetElementPosition[1] + 'px');
  z-index: 25;
  transition: 0.2s;
}
 #tooltip{
   width: v-bind(tooltipWidth);
   font-family: inherit;
   height: auto;
   box-sizing: border-box;
   padding: 10px 20px;
   text-align: center;
   z-index: 20;
   background-color: v-bind(tooltipStyling[1]);
   border: v-bind(tooltipStyling[2]);
   border-radius: v-bind(tooltipStyling[3]);
 }
 .pointerEventsDisabled{
   pointer-events: none;
 }
 span{
   color: v-bind(tooltipStyling[0]);
 }
 .visible{
   opacity: 1 !important;
 }
</style>