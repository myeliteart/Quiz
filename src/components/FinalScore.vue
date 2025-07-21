<template>
    <div class="border-y-5 border-amber-800 bg-white mt-5 py-9">
        <div>
            <h3 class="text-2xl sm:text-3xl md:text-5xl">Congratulations!</h3>
            <div class="max-w-[350px] md:max-w-[650px] mx-auto mt-8 font-medium text-amber-800">
               {{ `You had ${correct} answer/s out of ${quizy.question.length} questions correct` }}
            </div>
        </div>
        <button @click="$emit('start-again')" class="bg-amber-800 hover:bg-amber-900 text-white font-medium py-2 px-7 my-7 rounded-full text-lg cursor-pointer">Start Over</button>
    </div>
</template>

<script setup>
    const emit = defineEmits(['start-again'])
    const props = defineProps(['correct', 'quizy'])
</script>