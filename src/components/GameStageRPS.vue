<template>
  <SelectionBox :options="selectionBoxOptions" @selection="handleResult" />

  <button :disabled="isDisabled" @click="startGame">Start</button>
  <div class="playerbox">
    <div class="playerbox__player playerbox__player--one">
      {{ currentSelection }}
    </div>
    <div class="playerbox__player playerbox__player--two">
      {{ randomEmoji }}
    </div>
  </div>
  <p>{{ countWinsPlayer1 }} / {{ countWinsPlayer2 }}</p>
  <p>{{ winnerText }}</p>
  <button @click="newGame">Start new game</button>
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
      countWinsPlayer1: 0,
      countWinsPlayer2: 0,
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

    isDisabled() {
      if (this.countWinsPlayer1 >= 3 || this.countWinsPlayer2 >= 3) {
        return true;
      }
      return false;
    },
  },

  methods: {
    handleResult(currentItem) {
      this.selectedOption = currentItem;
      this.randomEmoji = "";
    },

    countWins() {
      if (this.selectedOption === this.randomOptionOutput) {
        this.countWinsPlayer1, this.countWinsPlayer2;
      } else {
        options[this.selectedOption].losingAgainst !== this.randomOptionOutput
          ? this.countWinsPlayer1++
          : this.countWinsPlayer2++;
      }
    },
    getWinner() {
      if (this.countWinsPlayer1 === 3) {
        this.winnerText = "Congrats, You won!";
      }
      if (this.countWinsPlayer2 === 3) {
        this.winnerText = "You lost. Try again!";
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
        this.countWins();
        this.getWinner();
      }
    },

    newGame() {
      window.location.reload();
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
