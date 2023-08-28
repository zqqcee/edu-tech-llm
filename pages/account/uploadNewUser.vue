<script setup>
import * as XLSX from 'xlsx/xlsx.mjs';
const { $i18n } = useNuxtApp()
definePageMeta({
  middleware: ["auth"],
  layout: 'vuetify-app',
})
const uploadForm = ref(null)
const userData = ref({
  file: [],
  new_file: '',
  new_file_name: 'None'
})
// const userData = ref(null)
const submitting = ref(false)
const downloading = ref(false)
const errorMsg = ref(null)

const rules = ref([
    v => !!v || 'File is required',
    v => (v && v.length > 0) || 'File is required',
])

var file = null

const uploadFile = async () => {
  const reader = new FileReader();
  reader.readAsDataURL(userData.value.file[0]);
  reader.onload = () => {
    file = reader.result
  };
}

const json2excel = (json_file) => {
  var filename = 'new_user_code.xlsx'
  var worksheet = XLSX.utils.json_to_sheet(json_file)
  var workbook = XLSX.utils.book_new()
  XLSX.utils.book_append_sheet(workbook, worksheet, "Sheet1");
  console.log('workbook')
  console.log(workbook)
  console.log('worksheet')
  console.log(worksheet)

  return [ workbook, filename ]
}

const submit = async () => {
  errorMsg.value = null
  const { valid } = await uploadForm.value.validate()

  if (valid && file) {
    submitting.value = true
    const formData = new FormData()
    formData.append('file', userData.value.file[0])

    const { data, error } = await useFetch('/api/account/uploadNewUser/', {
      method: 'POST',
      body: formData
    })

    if (error.value) {
      console.log(error.value)
      if (error.value.status === 400) {
        for (const key in formData.value) {
          if (error.value.data[key]) {
            fieldErrors.value[key] = $i18n.t(error.value.data[key][0])
          }
        }
        if (error.value.data.non_field_errors) {
          errorMsg.value = $i18n.t(error.value.data.non_field_errors[0])
        }
      } else {
        if (error.value.data.detail) {
          errorMsg.value = $i18n.t(error.value.data.detail)
        } else {
          errorMsg.value = $i18n.t('Something went wrong. Please try again.')
        }
      }
    } else {
      console.log('success!')
      console.log(data.value)
      
      var [ workbook, filename ] = json2excel(data.value)
      userData.value.new_file = workbook
      userData.value.new_file_name = filename
    }

    submitting.value = false
  }
}

const download = () => {
  downloading.value = true
  XLSX.writeFile(userData.value.new_file, userData.value.new_file_name)
  downloading.value = false
}

</script>

<template>
    <v-card
        style="height: 100vh"
    >
      <v-container>
        <v-row>
          <v-col
              sm="9"
              offset-sm="1"
              md="6"
              offset-md="3"
          >
            <v-card
                class="mt-15"
                elevation="0"
            >
              <div class="text-center text-h4">{{$t('Upload new user profiles')}}</div>
                <v-form ref="uploadForm" class="mt-5">
                  <v-file-input 
                    v-model="userData.file"
                    label="Upload only excel files" 
                    accept=".xlsx,.xls"
                    show-size
                    :rules="rules"
                    @change="uploadFile"
                  ></v-file-input>
                </v-form>
              
                <v-btn
                  size="large"
                  color="primary"
                  :loading="submitting"
                  @click="submit"
                >{{$t('submit')}}</v-btn>

                <div v-if="errorMsg" class="text-red">{{ errorMsg }}</div>

                <v-text-field
                  variant="outlined"
                  readonly
                >{{ userData.new_file_name }}</v-text-field>

                <v-btn
                  size="large"
                  color="primary"
                  :loading="downloading"
                  @click="download"
                >{{$t('download')}}</v-btn>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-card>
  </template>

