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
          img: 'https://www.metabunk.org/attachments/oval-office-jpg.42994/'
        },
        {
          qutn: 'In what year did World War II end?',
          img: 'https://www.nationalww2museum.org/sites/default/files/styles/wide_medium/public/2023-08/liberationofparis.png?h=7398e27f'
        },
        {
          qutn: 'What is your favorite front-end programming language?',
          img: 'https://www.simplilearn.com/ice9/free_resources_article_thumb/recact_angular_vue.jpg'
        },
        {
        qutn: 'Whats the capital of Canada?',
        img: 'https://www.taylorstracks.com/wp-content/uploads/2018/01/Ottawa-Rideau-Canal.jpg.webp'
      },
      {
        qutn: 'What is your favorite color?',
        img: 'https://img.freepik.com/premium-photo/abstract-colorful-background-elegant-design-cover-modern-composition_1145931-59506.jpg?semt=ais_hybrid&w=740'
      },
      {
        qutn: 'In which us city is Disney World located',
        img: 'https://www.thetopvillas.com/blog/wp-content/uploads/2021/05/Webp.net-resizeimage-2021-05-25T162018.092-1.jpg'
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