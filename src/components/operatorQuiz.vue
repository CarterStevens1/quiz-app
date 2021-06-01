<template>
  <div>
    <div v-if="isStarted">
      <h4>{{ operandLeft }} {{ operator }} {{ operandRight }}</h4>
      <button
        @click="selectAnswer(answer)"
        v-for="(answer, index) of answers"
        :key="index"
      >
        {{ answer }}
      </button>
    </div>

    <div v-if="!isStarted">
      <button @click="startQuiz">Start</button>
    </div>
    <button @click="$emit('onBack')">Back</button>
  </div>
</template>

<script>
export default {
  props: ["operator"],
  data() {
    return {
      isStarted: false,
      operandLeft: null,
      operandRight: null,
      answers: [],
      expectedAnswer: null,

      lastAnswer: [],
    };
  },
  methods: {
    selectAnswer(answerSelected) {
      if (answerSelected !== this.expectedAnswer) {
        alert("Wrong Answer, Try again!");
      } else {
        this.startQuiz();
      }
    },
    startQuiz() {
      this.isStarted = true;
      this.operandLeft = parseInt(Math.random() * 13);
      this.operandRight = parseInt(Math.random() * 13);

      const methods = {
        "+": (a, b) => a + b,
        "-": (a, b) => a - b,
        "/": (a, b) => a / b,
        "*": (a, b) => a * b,
      };

      const methodToUse = methods[this.operator];

      this.answers = [];
      this.lastAnswer = [];

      const expectedAnswer = methodToUse(this.operandLeft, this.operandRight);
      let i = 0;

      while (i < 5) {
        const answer = methodToUse(
          parseInt(Math.random() * 13),
          parseInt(Math.random() * 13)
        );

        let allowedNumber = true;
        for (let n = 0; n < this.answers.length; n++) {
          if (answer == this.answers[n] || answer == expectedAnswer) {
            allowedNumber = false;
          }
        }

        if (allowedNumber) {
          this.answers.push(answer);
          i++;
        }
      }

      this.answers[
        parseInt(Math.random() * this.answers.length)
      ] = expectedAnswer;
      this.expectedAnswer = expectedAnswer;
    },
  },
};
</script>

<style></style>
