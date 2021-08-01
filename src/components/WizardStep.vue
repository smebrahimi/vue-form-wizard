<template>
  <li :class="{active:tab.active}">
    <a href="javascript:void(0)" :class="{disabled: !tab.checked}">
      <div class="container-wizard-icon-circle">
        <div class="wizard-icon-circle md"
            role="tab"
            :tabindex="tab.checked ? 0 : ''"
            :id="`step-${tab.tabId}`"
            :aria-controls="tab.tabId"
            :aria-disabled="tab.active"
            :aria-selected="tab.active"
            :class="{checked: tab.checked,square_shape:isStepSquare, tab_shape:isTabShape}"
            :style="tab.checked && !tab.active ? stepCheckedStyle : {}">

          <transition :name="transition" mode="out-in">
              <div v-if="tab.active" class="wizard-icon-container"
                  :class="{square_shape:isStepSquare, tab_shape:isTabShape}"
                  :style="tab.active ? iconActiveStyle: {}">
                <slot name="active-step">
                  <span v-if="tab.icon" :class="tab.icon" class="wizard-icon"></span>
                  <span v-else class="wizard-icon" :style="[tab.active ? textActiveStyle : {}]">{{index + 1}}</span>
                </slot>
              </div>
              <slot v-if="!tab.active">
                <span v-if="tab.checked && !tab.validationError" :class="tab.icon" class="wizard-icon ti-check icomoon-check"></span>
                <span v-if="tab.checked && tab.validationError" :class="tab.icon" class="wizard-icon xx">{{index + 1}}</span>
                <span v-if="!tab.active && !tab.icon" :class="tab.icon" class="wizard-icon">{{index + 1}}</span>
              </slot>
          </transition>

        </div>
      </div>
      <slot name="title">
        <span class="stepTitle"
              :class="{active:tab.active}"
              :style="tab.active || tab.checked ? textActiveStyle : {}">
              {{tab.title}}
        </span>
      </slot>
    </a>
  </li>
</template>
<script>
  export default {
    name: 'wizard-step',
    props: {
      tab: {
        type: Object,
        default: () => {

        }
      },
      transition: {
        type: String,
        default: ''
      },
      index: {
        type: Number,
        default: 0
      }
    },
    computed: {
      iconActiveStyle () {
        return {
          backgroundColor: '#D6E13A' // active color
        }
      },
      textActiveStyle () {
        return {
          color: '#265C1F'
        }
      },
      stepCheckedStyle () {
        return {
          color: 'white',
          backgroundColor: '#265C1F' // success color
        }
      },
      isStepSquare () {
        return this.tab.shape === 'square'
      },
      isTabShape () {
        return this.tab.shape === 'tab'
      }
    }
  }
</script>
<style>
</style>
