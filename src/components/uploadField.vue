<template>
  <div class="upload-field">
    <div class="inputs-wrapper">
      <input
        accept="image/*,audio/*,video/*,text/*"
        type="file"
        id="input-file"
        hidden
        ref="fileInputFieldRef"
        @change="fileInputChangeHandler"
      />
      <input
        type="text"
        id="input-text"
        class="input-text"
        disabled
        ref="textInputFieldRef"
        placeholder="e.g. file.txt"
      />
      <button id="insert-button" class="green-button" @click="handleInsert" v-if="!insertedFile">
        INSERT
      </button>
      <button
        type="submit"
        id="upload"
        class="green-button"
        :class="{ upload: insertedFile }"
        @click="handleUpload"
        v-if="insertedFile"
      >
        UPLOAD
      </button>
      <button id="cancel" class="red-button" @click="handleCancel" v-if="insertedFile">
        <font-awesome-icon :icon="faXmark" size="xl" />
      </button>
    </div>
    <div class="upload-field-text">
      <p>Or drag & drop here!</p>
    </div>
  </div>
</template>

<style scoped>
.upload-field {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 255, 170, 0.075);
  width: 50rem;
  height: 20rem;
  border: dashed;
  border-radius: 8px;
  border-color: var(--color-border-hover);
  transition-duration: 200ms;
}
.upload-field:hover {
  background-color: rgba(0, 255, 170, 0.13);
}
.inputs-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}
.input-text {
  min-width: 20rem;
  height: 3.2rem;
  border-radius: 5px 0px 0px 5px;
  background: rgba(0, 255, 170, 0.075);
  border-style: solid;
  border-width: 3px;
  border-color: hsla(160, 100%, 37%, 1);
  outline: none;
  transition-duration: 200ms;
  color: white;
  text-overflow: ellipsis;
  padding-left: 0.5rem;
  font-size: medium;
}
.input-text::placeholder {
  color: rgb(168, 168, 168);
}
.input-text:hover {
  background: rgba(0, 255, 170, 0.274);
}
.upload {
  border-radius: 0px 0px 0px 0px !important;
}
.green-button {
  cursor: pointer;
  font-size: 1rem;
  height: 3.2rem;
  background-color: hsla(160, 100%, 37%, 1);
  border: none;
  color: white;
  border-radius: 0px 4px 4px 0px;
  padding: 0 2rem 0 2rem;
  font-weight: bold;
  transition-duration: 100ms;
}
.green-button:hover {
  background-color: rgb(34, 212, 153);
}

.red-button {
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  font-size: 1rem;
  height: 3.2rem;
  background-color: rgb(224, 45, 45);
  border: none;
  color: white;
  border-radius: 0px 4px 4px 0px;
  padding: 0 1.5rem 0 1.5rem;
  font-weight: bold;
  transition-duration: 100ms;
}
.red-button:hover {
  background-color: rgb(255, 60, 60);
}
</style>
<script setup lang="ts">
import { toast } from 'vue3-toastify'
import 'vue3-toastify/dist/index.css'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faXmark } from '@fortawesome/free-solid-svg-icons'
import { ref } from 'vue'

const fileInputFieldRef = ref<HTMLInputElement | null>(null)
const insertedFile = ref<File | null>(null)
const textInputFieldRef = ref<HTMLInputElement | null>(null)
const handleInsert = () => {
  if (!fileInputFieldRef.value) return
  fileInputFieldRef.value.click()
}
const notify = () => {
  toast('Wow so easy !', {
    autoClose: 1000
  }) // ToastOptions
}
//TODO: Handle file drop
// const handleFileDrop = (event: DragEvent) => {
//   event.preventDefault()
//   if (!insertedFile.value) return
//   //TODO: Create drag & drop field functionality.
//   // insertedFile.value = event.dataTransfer?.files[0]
// }
const fileInputChangeHandler = () => {
  if (!fileInputFieldRef.value || !fileInputFieldRef.value.files) return
  insertedFile.value = fileInputFieldRef.value.files[0]
  if (!textInputFieldRef.value) return
  textInputFieldRef.value.value = insertedFile.value.name
}
const handleUpload = async (event: Event) => {
  event.preventDefault()
  const formData = new FormData()
  if (!insertedFile.value || !fileInputFieldRef.value || !textInputFieldRef.value) return
  formData.append('File', insertedFile.value)
  try {
    const res = await fetch('http://localhost:3000/file/up_file', {
      method: 'POST',
      body: formData,
      mode: 'no-cors' //for now.
    })
    console.log(res)
    fileInputFieldRef.value.value = ''
    insertedFile.value = null
    textInputFieldRef.value.value = ''
  } catch (error) {
    console.log(error)
  }
}
const handleCancel = () => {
  if (!fileInputFieldRef.value || !textInputFieldRef.value) return
  fileInputFieldRef.value.value = ''
  insertedFile.value = null
  textInputFieldRef.value.value = ''
}
</script>
