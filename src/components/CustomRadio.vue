<template lang="pug">
div.radio-group
  label.custom-radio
    input(type="radio" name="example" value="1" v-model="selected")
    span.radio-label
    span.radio-text 选项一

  label.custom-radio
    input(type="radio" name="example" value="2" v-model="selected")
    span.radio-label
    span.radio-text 选项二

  label.custom-radio
    input(type="radio" name="example" value="3" v-model="selected")
    span.radio-label
    span.radio-text 选项三
</template>

<script setup lang="ts">
import { ref } from 'vue'

const selected = ref('1')
</script>

<style lang="scss">
@import '../assets/styles/radio.scss';
</style> 