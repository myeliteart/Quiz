<template>
  <div class="max-w-[750px] mx-auto text-center px-7 md:px-0 my-16 items-center justify-center">
    <div class="flex justify-between items-center">
       <h2 class="text-3xl font-bold text-amber-800">Quiz Challenge</h2>
       <p v-if="count <= quizy.question.length">{{ count }} of {{ quizy.answers.length }}</p>
    </div>
    <quiz v-if="index < quizy.question.length" :quizy="quizy" :start="start" :next="next" :selectedAnswer="selectedAnswer" :index="index"  @startTheQuiz="starting" @theAnswer="theAnswer" @nxt="nxtSlide"></quiz>
    <final-score v-else :correct="correct" :quizy="quizy" @start-again="again"></final-score>
  </div>
</template>

<script setup>
  import quiz from './components/quiz.vue';
  import FinalScore from './components/FinalScore.vue';
  import { ref, watch } from 'vue';

  const index = ref(0);
  const count = ref (0);
  const correct = ref(0);
  let quizy = ref (
    {
      question: [
        {
          qutn: 'Who is currently the president of the united states?',
          img: 'https://media.npr.org/assets/img/2021/01/21/ap_21021110780453_custom-d6dfddf768dbd02ed59154c961a2f7f9a6fbcaff.jpg?s=1100&c=50&f=jpeg'
        },
        {
          qutn: 'In what year did World War II end?',
          img: 'https://m.media-amazon.com/images/I/71JRYtkJx1L._UF894,1000_QL80_.jpg'
        },
        {
          qutn: 'What is your favorite front-end programming language?',
          img: 'https://media.licdn.com/dms/image/v2/D4D12AQESYQmZS5KNbg/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1690841770785?e=2147483647&v=beta&t=scQnI6hOtuhHTxuKOua45QpFaw5el2SCdtGADnN2ab0'
        },
        {
        qutn: 'Whats the capital of Canada?',
        img: 'https://guias-viajar.com/wp-content/uploads/2014/07/Fotos-Canada-Ottawa-002-2.jpg'
      },
      {
        qutn: 'What is your favorite color?',
        img: 'https://cdn.apartmenttherapy.info/image/upload/v1657303275/at/art/design/2022-07/Color-Month/Colormonth-mood-3000x2000.png'
      },
      {
        qutn: 'In which us city is Disney World located',
        img: 'https://res.klook.com/images/fl_lossy.progressive,q_65/c_fill,w_1200,h_630/activities/avkqwz1ar2964muauoml/Walt%20Disney%20World%20Resort%20Ticket.jpg'
      }
    ],
      answers: [
        {
          1: 'Donald Trump',
          2: 'John Kenedy',
          3: 'Barack Obama',
          4: 'Thomas Jefferson' 
        },
        {
          1: '1939',
          2: 'Im not sure',
          3: '1945',
          4: '1951'
        },
        {
          1: 'Angular',
          2: 'Svelte',
          3: 'React',
          4: 'Vue js'
        },
         {
          1: 'Montreal',
          2: 'Quebec',
          3: 'Ottawa',
          4: 'Toronto'
        },
        {
          1: 'Green',
          2: 'Yellow',
          3: 'Purple',
          4: 'Red'
        },
        {
          1: 'Los Angeles',
          2: 'Florida',
          3: 'Los Vagas',
          4: 'New york City'
        }
      ],
      correctAnswer: ['Donald Trump', '1945', 'Vue js', 'Ottawa', 'Purple', 'Florida']
    }
  )
   let selectedAnswer = ref(null);

   const next = ref (false)

   const theAnswer = (answer) => {
    next.value = true
    selectedAnswer.value = answer
  }
  const nxtSlide = () => {
    index.value++
    next.value = false
    count.value++
    // if(correctAnswer.value.includes(selectedAnswer.value)) {
      
    // }
  }
  const start = ref(true)

  const starting = () => {
    start.value = false
    count.value = 1
  }

  const again = () => {
    start.value = false
    index.value = 0
    next.value = false
    count.value = 1
    correct.value = 0
    selectedAnswer.value = null
  }

  // const checkTheScore = computed(() => {
  //   if(quizy.value.correctAnswer.includes(selectedAnswer.value)){
  //     return 1111
  //   } else {
  //     return 15
  //   }
  // })

   watch(selectedAnswer, (newVal, oldVal) => {
      if(quizy.value.correctAnswer.includes(newVal)){
        console.log(`hello: ${newVal}`)
        correct.value++
      }
    })
</script>