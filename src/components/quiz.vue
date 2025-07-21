<template>
    <div class="border-y-5 border-amber-800 bg-white mt-4 py-7">
        <div v-if="!start">
            <div v-for="itm in quizy.question.slice(index, index + 1)">
                <h3 class="text-2xl px-10 md:px-0">{{ itm.qutn }}</h3>
                <img :src="itm.img" class="mt-6 w-full">
            </div>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-5 mx-auto px-11 py-6">
                <div v-for="(answer, index) in quizy.answers[index]" :key="answer" @click="chooseAnswer(answer)" :class="{'border bg-amber-800 text-white border-amber-700 hover:border-amber-900 rounded-full w-full py-3 text-lg cursor-pointer': selectedAnswer == answer}" class="border border-amber-700 hover:border-amber-900 rounded-full w-full py-3 text-lg cursor-pointer">
                   <div class="flex items-center place-self-center">
                     <div class="font-bold w-8 h-8 border items-center rounded-full mr-3">{{ index }}</div>
                     <div>{{ answer }}</div>
                   </div>              
                </div>
            </div>
              
        </div>
        <button v-else @click="emit('startTheQuiz')" class="bg-amber-800 hover:bg-amber-900 text-white font-medium py-3 px-8 my-7 rounded-full text-lg cursor-pointer">Start Quiz</button>
        <button v-if="next" @click="emit('nxt')" class="bg-transpernt border text-amber-900 border-amber-900 hover:bg-amber-900 hover:text-white font-medium py-3 px-8 my-6 rounded-full text-lg cursor-pointer">Next Question</button>
    </div>
</template>

<script setup>    
    const props = defineProps(['quizy', 'start', 'next', 'selectedAnswer', 'index'])
    const emit = defineEmits(['startTheQuiz', 'theAnswer', 'nxt'])

    const chooseAnswer = (answer) => {
        emit('theAnswer', answer)
    }
</script>