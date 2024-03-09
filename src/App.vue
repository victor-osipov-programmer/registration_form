<template>
    <div class="max-w-[700px] w-full mt-10 mb-16 mx-auto">
        <RegistrationForm />
        <!-- <button @click="close">Закрыть</button> -->
    </div>
</template>

<script setup>
import { onMounted } from "vue";
import RegistrationForm from "./components/RegistrationForm.vue";
const tg = window.Telegram.WebApp;
console.log();
if (tg.colorScheme == 'dark') { // tg.colorScheme == 'dark'
    document.documentElement.classList.add('dark')
}
// if (tg) {
//   
// } else {
//   document.documentElement.classList.remove('dark')
// }

onMounted(() => {
    tg.ready()
})

const close = () => {
    tg.close()
}
</script>
