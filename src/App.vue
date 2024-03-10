<template>
    <div class="max-w-[700px] w-full mt-10 mb-16 mx-auto">
        <RegistrationForm />
    </div>
</template>

<script setup>
import { onMounted } from "vue";
import RegistrationForm from "./components/RegistrationForm.vue";
const tg = window.Telegram.WebApp;

// if (1) {
//     document.documentElement.classList.add('dark')
// }
if (tg.colorScheme == 'dark') {
    document.documentElement.classList.add('dark')
}

onMounted(() => {
    tg.ready()
})
</script>
