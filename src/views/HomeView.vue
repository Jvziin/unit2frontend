<script setup>
import{ onMounted, ref } from 'vue'
import { useCookies } from 'vue3-cookies'
import { decodeCredential, googleLogout } from 'vue3-google-login'

const { cookies } = useCookies()

let isLoggedIn = ref(false)
let userName = ''

const callback = (response) => {
    isLoggedIn.value = true
    const userData = decodeCredential(response.credential)
    console.log(userData)
    userName = userData.given_name
    cookies.set('user_session', response.credential)
    fetch(`${import.meta.env.VITE_API_URL}`, {
        method: "POST",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify({
            userEmail: userData.userEmail
        })
    })
    .then(() => {
        console.log('session saved')
    })
    .catch(err => console.error(err))
}

const checkSession = () => {
    if (cookies.isKey('user_session')) {
        isLoggedIn.value = true
        const userData = decodeCredential(cookies.get('user_session'))
        userName = userData.given_name
    }
}

const handleLogout = () => {
    googleLogout()
    cookies.remove('user_session')
    isLoggedIn.value = false
}

onMounted(checkSession)

</script>
<template>

</template>
