<template>
  <div>
    <v-row>
      <v-col cols="7" class="bg-white">
        <div class="backgroundImg">
        </div>
      </v-col>
      <v-col cols="5" class="bg-white">
        <div class="loginContainer">
          <div class="text-center text-h3 text-black signInTitle">{{ $t('signIn') }}</div>
          <div class="text-center text-h7 text-grey signInSubTitle">智能引领，教育创新</div>
          <v-card color="#fff" class="signInCard">
            <v-card-text>
              <v-form ref="signInForm">
                <v-text-field class="signInInput text-black" v-model="formData.username" :rules="formRules.username"
                  :label="$t('username')" clearable></v-text-field>
                <v-text-field class="signInInput" v-model="formData.password" :rules="formRules.password"
                  :label="$t('password')" @keyup.enter="submit" clearable :type="passwordInputType"
                  :append-inner-icon="passwordInputType === 'password' ? 'visibility' : 'visibility_off'"
                  @click:append-inner="passwordInputType = passwordInputType === 'password' ? 'text' : 'password'"></v-text-field>
              </v-form>

              <div v-if="errorMsg" class="text-red">{{ errorMsg }}</div>

              <div class="signUpBlock">
                <v-row justify="flex-end">
                  <v-col cols="6">
                    <v-btn @click="navigateTo('/account/signup')" variant="text" color="primary">{{ $t('createAccount')
                    }}</v-btn>
                  </v-col>
                  <v-col cols="6" class="text-right">
                    <v-btn @click="navigateTo('/account/resetPassword?reason=forgetPassword')" variant="text"
                      color="primary">{{ $t('forgetPassword') }}</v-btn>
                  </v-col>
                </v-row>
              </div>

              <div class="signInBtn">
                <v-btn block color="primary" :loading="submitting" @click="submit" size="large">{{ $t('signIn') }}</v-btn>
              </div>

            </v-card-text>
          </v-card>

        </div>
      </v-col>
    </v-row>
    <div class="logoImg">

    </div>
  </div>
</template>

<script setup>
const { $i18n } = useNuxtApp()
definePageMeta({
  layout: 'vuetify-app'
})
const formData = ref({
  username: '',
  password: ''
})
const formRules = ref({
  username: [
    v => !!v || $i18n.t('Username is required')
  ],
  password: [
    v => !!v || $i18n.t('Password is required')
  ]
})
const errorMsg = ref(null)
const signInForm = ref(null)
const submitting = ref(false)
const route = useRoute()
const passwordInputType = ref('password')

const submit = async () => {
  errorMsg.value = null
  const { valid } = await signInForm.value.validate()
  if (valid) {
    submitting.value = true
    // const { data, error } = await useFetch('/api/account/login/', {
    //   method: 'POST',
    //   body: JSON.stringify(formData.value)
    // })
    submitting.value = false
    // if (error.value) {
    //   if (error.value.status === 400) {
    //     if (error.value.data.non_field_errors) {
    //       errorMsg.value = error.value.data.non_field_errors[0]
    //     }
    //   } 
    //   else {
    //     if (error.value.data.detail) {
    //       errorMsg.value = $i18n.t(error.value.data.detail)
    //     } 
    //     else {
    //       errorMsg.value = $i18n.t('Something went wrong. Please try again.')
    //     }
    //   }
    // } 
    // else {
    //   setUser(data.value.user)
    //   const callback = route.query.callback ? decodeURIComponent(route.query.callback) : '/'
    //   await navigateTo(callback)
    // }

    // const callback = route.query.callback ? decodeURIComponent(route.query.callback) : '/'
    // await navigateTo(callback)
    navigateTo('/')
  }
}

</script>

<style>
.backgroundImg {
  background-color: black;
  height: 100vh;
  background-image: url('../../assets/bg-img.jpeg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}

.logoImg {
  width: 200px;
  height: 80px;
  position: absolute;
  border-radius: 20px;
  border: 1px solid rgba(0, 0, 0, 0.182);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  top: 0;
  right: 0;
  background-image: url('../../assets/bottle.svg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}

.loginContainer {
  margin-top: 250px;
}

.signInTitle {
  padding-bottom: 10px;
}

.signInSubTitle {
  padding-bottom: 50px;
}

.signInCard {
  border: 1px solid #f6f6f6;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
  transition-property: box-shadow;
  transition-duration: .3s;
  transition-timing-function: ease;
}

.signInCard:hover {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  border: 1px solid #e8dede;
  transition-property: box-shadow;
  transition-duration: .3s;
  transition-timing-function: ease;
}

.signInInput {
  padding: 20px;
  background-color: #ffffff !important;
}

.signInInputActiveClass {
  background-color: #fff;
}

.signInBtn {
  padding-top: 20px;
}

.bg-white {
  background-color: #fff;
}
</style>