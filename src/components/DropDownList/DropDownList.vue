<template>
  <div class="dropdown">
    <a href="#" class="btn btn-outline-light my-2 dropdown-toggle" @click.prevent="toggleOpen">{{title}}</a>
    <ul class="dropdown-menu" style="display:block" v-if="isOpen">
        <slot/>
    </ul>
  </div>
</template>

<script lang="ts">

import { defineComponent, ref } from 'vue'

// upload a image file to server
// @param file: file object
// @param url: url to upload
// return a promise
export function uploadFile (file: File, url: string): Promise<any> {
  return new Promise((resolve, reject) => {
    const formData = new FormData()
    formData.append('file', file)
    const xhr = new XMLHttpRequest()
    xhr.open('POST', url, true)
    xhr.onload = function () {
      if (this.status === 200) {
        resolve(JSON.parse(this.response))
      } else {
        reject(this.statusText)
      }
    }
    xhr.onerror = function () {
      reject(this.statusText)
    }
    xhr.send(formData)
  })
}

// display a image file
// @param url: url to display
// return a promise
export function displayImage (url: string): Promise<any> {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest()
    xhr.open('GET', url, true)
    xhr.responseType = 'blob'
    xhr.onload = function () {
      if (this.status === 200) {
        resolve(this.response)
      } else {
        reject(this.statusText)
      }
    }
    xhr.onerror = function () {
      reject(this.statusText)
    }
    xhr.send()
  })
}

export default defineComponent({
  name: 'DropDownList',
  props: {
    title: {
      type: String,
      required: true
    }
  },
  setup (props) {
    const isOpen = ref(false)
    const toggleOpen = () => {
      isOpen.value = !isOpen.value
    }
    return {
      isOpen,
      toggleOpen
    }
  }
})

</script>

<style>

</style>
