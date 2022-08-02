<template>
  <SelectionBox :options="selectionBoxOptions" @selection="handleResult" />

  <button @click="startGame">Start</button>
  <div class="playerbox">
    <div class="playerbox__player playerbox__player--one">
      {{ currentSelection }}
    </div>
    <div class="playerbox__player playerbox__player--two">
      {{ randomEmoji }}
    </div>
  </div>
  <p>{{ winnerText }}</p>
</template>

<script>
import SelectionBox from "./SelectionBox.vue";

const options = {
  rock: { label: "rock", emoji: "👊", losingAgainst: "paper" },
  paper: { label: "paper", emoji: "✋", losingAgainst: "scissor" },
  scissor: { label: "scissor", emoji: "✌", losingAgainst: "rock" },
};
export default {
  components: {
    SelectionBox,
  },
  data() {
    return {
      selectionBoxOptions: [
        {
          value: "",
          text: "Please select...",
        },
        {
          value: "rock",
          text: "Rock",
        },
        {
          value: "paper",
          text: "Paper",
        },
        {
          value: "scissor",
          text: "Scissor",
        },
      ],
      selectedOption: "",
      randomEmoji: "",
      randomOptionOutput: "",
      winnerText: "Good Luck!",
    };
  },

  computed: {
    currentSelection() {
      if (this.selectedOption !== "") {
        return options[this.selectedOption].emoji;
      } else {
        return "";
      }
    },
  },

  methods: {
    handleResult(currentItem) {
      this.selectedOption = currentItem;
    },
    getWinner() {
      if (this.selectedOption === this.randomOptionOutput) {
        this.winnerText = "Draw!";
      } else {
        this.winnerText =
          options[this.selectedOption].losingAgainst !== this.randomOptionOutput
            ? "You win"
            : "You loose";
      }
    },
    getRandomEmoji(itemLength) {
      const index = Math.floor(Math.random() * itemLength);
      const randomOption = Object.keys(options)[index];
      this.randomOptionOutput = randomOption;
      this.randomEmoji = options[randomOption].emoji;
    },

    startGame() {
      const itemLength = Object.keys(options).length;

      if (this.selectedOption === "") {
        alert("choose an emoji");
      } else {
        this.getRandomEmoji(itemLength);
        this.getWinner();
      }
    },
  },

  watch: {
    selectedOption(currentValue) {
      if (currentValue === "") {
        this.winnerText = "";
        this.randomEmoji = "";
      }
    },
  },
};
</script>

<style scoped>
.playerbox {
  display: flex;
  justify-content: center;
}
.playerbox__player {
  border: black double;
  height: 10rem;
  width: 10rem;
  margin: 2rem;
  font-size: 6rem;
}
</style>
