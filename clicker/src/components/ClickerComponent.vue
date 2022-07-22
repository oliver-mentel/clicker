<template>
  <!-- Countdown Timer -->
  <div class="item-container">
    <div class="countdown-container">
      <div class="timer-container">
        <p class="time-font">{{ isTimerReseted ? 10 : countDown }}s</p>
      </div>
    </div>
    <h3 v-if="isBestScore && displayInfo" class="high-score-text">
      !!! NEW HIGH SCORE !!!
    </h3>
    <!-- Click sum text -->
    <h4 style="margin-bottom: 10px">You clicked {{ clicks }} times.</h4>
    <br />

    <!-- Click Button -->
    <button
      :disabled="countDown <= 0 && countDown === 10"
      @click="clickIterator()"
      class="button"
    >
      Click
    </button>
    <br />

    <!-- Info -->
    <div class="info-container">
      <h4 v-if="displayInfo && !isBestScore" class="good-effort-text">
        {{ getRank + 1 === (2 || 3) ? "Not Bad!" : "" }}
        {{ userName }}!
        <br />
        You made #{{ getRank + 1 }} position!
        <br />
        Better luck next time...
      </h4>
      <!-- Click/ Time Ratio -->
      <h4 v-if="displayInfo" class="ratio-text">
        Your click over time ratio: {{ clicks / 10 }} clicks / s
      </h4>
    </div>
    <!-- Reset Button -->
    <button @click="resetAllValues()">Reset</button>

    <!-- Top Scorte Heading & List -->
    <div class="top-score-container">
      <h2 class="top-score-title">
        Top {{ orderedHighScoresAndUsers.length === 9 ? "10" : "" }} Scores
      </h2>
      <ol class="list">
        <li
          v-for="(user, index) in orderedHighScoresAndUsers"
          :class="colorRankByIndex(index)"
        >
          <div class="score-item">
            <div>{{ user.score }}</div>
            <div>{{ user.name }}</div>
          </div>
        </li>
        <p v-if="orderedHighScoresAndUsers.length === 0">
          No Scores to Display
        </p>
      </ol>
    </div>
  </div>
</template>

<script>
export default {
  name: "ClickerComponent",
  props: {
    msg: String,
    userName: String,
  },
  data() {
    return {
      clicks: 0,
      calories: 0,
      countDown: 10,
      colorRank: "",
      timerEnabled: false,
      displayInfo: false,
      isBestScore: false,
      isTimerReseted: false,
      orderedHighScoresAndUsers: [
        // {
        //   score: 10,
        //   name: this.userName,
        // },
      ],
    };
  },
  computed: {
    getRank() {
      return this.orderedHighScoresAndUsers.findIndex(
        (user) => user.score === this.clicks
      );
      //   return this.orderedHighScoresAndUsers.indexOf(this.clicks);
    },
  },

  methods: {
    colorRankByIndex(index) {
      if (index === 0) {
        return "gold";
      } else if (index === 1) {
        return "silver";
      } else if (index === 2) {
        return "bronze";
      } else {
        return "ranking-numbers";
      }
    },
    reduceArrayLength() {
      return this.orderedHighScoresAndUsers.slice(0, 9);
    },
    orderedTopScores() {
      // order high scores from orderedHighScoresAndUsers by descending order
      this.orderedHighScoresAndUsers.sort((a, b) => {
        return b.score - a.score;
      });
    },
    clickIterator() {
      if (this.clicks === 0) {
        this.timerEnabled = true;
        this.isTimerReseted = false;
        this.countDownTimer();
      }
      if (this.countDown > 0) {
        return this.clicks++;
      }
    },
    countDownTimer() {
      if (this.countDown > 0 && this.isTimerReseted) {
        this.displayInfo = false;
      } else if (this.countDown > 0 && this.timerEnabled) {
        setTimeout(() => {
          --this.countDown;
          this.countDownTimer();
        }, 1000);
      } else {
        this.displayInfo = true;
        this.appendTopScoreList();
      }
    },
    resetAllValues() {
      if (this.countDown !== 0) {
        this.countDown = 10;
      } else {
        this.countDown = 10;
      }
      this.isTimerReseted = true;
      this.calories, (this.clicks = 0);
      this.timerEnabled = false;
      this.displayInfo = false;
      this.isBestScore = false;
    },

    appendTopScoreList() {
      if (this.countDown === 0) {
        this.orderedHighScoresAndUsers.push({
          name: this.userName,
          score: this.clicks,
        });
        if (
          this.orderedHighScoresAndUsers[0].score < this.clicks ||
          this.orderedHighScoresAndUsers.length === 0
        ) {
          this.isBestScore = true;
        }
        // wait 3 seconds before prompting user to enter name

        console.log(this.orderedHighScoresAndUsers[0].score);
        this.orderedTopScores();
        if (this.orderedHighScoresAndUsers.length >= 9) {
          this.orderedHighScoresAndUsers.length = 10;
        }
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* Ranking colors for High Score list */
.item-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  flex-wrap: nowrap;
  align-content: center;
}

.gold {
  color: #ffd700;
  font-size: 35px;
  margin: 30px 10px;
  border-radius: 20px;
  background-color: rgb(255 255 0 / 5%);
  box-shadow: 0px 0px 12px 10px;
}
.silver {
  color: #c0c0c0;
  font-size: 30px;
  margin: 30px 15px;
  border-radius: 20px;
  background-color: rgb(255 255 0 / 5%);
  box-shadow: 0px 0px 12px 5px;
}
.bronze {
  color: #cd7f32;
  font-size: 25px;
  margin: 30px 20px;
  border-radius: 20px;
  background-color: rgb(255 255 0 / 5%);
  box-shadow: 0px 0px 12px 4px;
}
.ranking-numbers {
  margin: 10px 10px;
}
.list {
  position: relative;
  left: 0px;
  width: 70%;
  padding-left: 0px;
  font-size: 20px;
  font-family: "Roboto", sans-serif;
  font-weight: bold;
}
.score-item {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}

button,
.button {
  position: relative;
  padding: 10px 30px;
  margin: 30px;
  width: fit-content;
  border: 0px solid grey;
  border-radius: 20px;
  background-color: #fbab7e;
  overflow: hidden;
  font-size: 20px;
  color: #fff;
  cursor: pointer;
  transition: 0.2s all;
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none; /* Konqueror HTML */
  -moz-user-select: none; /* Old versions of Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none; /* Non-prefixed version, currently
  supported by Chrome, Edge, Opera and Firefox */
}
.button:active {
  transform: scale(0.98);
  /* Scaling button to 0.98 to its original size */
  box-shadow: 0px 5px 17px 4px rgb(0 0 0 / 24%);
  /* Lowering
 the shadow */
}
h5,
h4 {
  font-weight: 200;
}

/* High Score Text with keyframes */
.high-score-text {
  animation: color-change 1s infinite;
  -webkit-animation: color-change 1s infinite;
  font-size: 30px;
  font-size: 5.5vw;
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none; /* Konqueror HTML */
  -moz-user-select: none; /* Old versions of Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none; /* Non-prefixed version, currently
  supported by Chrome, Edge, Opera and Firefox */
}
@keyframes color-change {
  0% {
    color: #ff9a8b;
  }
  50% {
    color: #ff6a88;
  }
  100% {
    color: #ff99ac;
  }
}
@-webkit-keyframes color-change {
  0% {
    color: #ff9a8b;
  }
  50% {
    color: #ff6a88;
  }
  100% {
    color: #ff99ac;
  }
}
.countdown-container {
  background-color: #ff9a8b;
  background: #eee;
  width: fit-content;
  margin: 0 auto;
  padding: 10px 20px;
  /* color: linear-gradient(180deg, #ff9a8b 0%, #ff6a88 55%, #ff99ac 100%); */
  font-size: 72px;
  border-radius: 20px;
}
.timer-container {
  min-width: 60px;
  height: auto;
  margin: 10px 10px;
}
.time-font {
  font-size: 35px;
  font-weight: 300;
  text-align: center;
  padding: -10px;
  background: -webkit-linear-gradient(
    180deg,
    #ff9a8b 0%,
    #ff6a88 55%,
    #ff99ac 100%
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.info-container {
  display: flex;
  justify-content: center;
  flex-direction: column;
}

.top-score-container {
  /* border: 1px white solid;
  border-radius: 20px; */
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
  min-width: 500px;
  background: linear-gradient(
    135deg,
    rgba(255, 255, 255, 0.1),
    rgba(255, 255, 255, 0)
  );
  -webkit-backdrop-filter: blur(20px);
  box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
  border: 1px solid rgba(255, 255, 255, 0.18);
  border-radius: 32px;
}
.top-score-title {
  font-family: "Roboto", sans-serif;
  font-weight: 100;
  margin: 0px 0px 30px 0px;
  background: linear-gradient(
    135deg,
    rgba(255, 255, 255, 0.3),
    rgba(255, 255, 255, 0)
  );
  -webkit-backdrop-filter: blur(20px);
  /* box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37); */
  border-bottom: 1px solid rgba(255, 255, 255, 0.18);
  -webkit-border-bottom: 1px solid rgba(255, 255, 255, 0.18);
  -webkit-border-radius: 0px 0px 20px 20px;
  width: fit-content;
  padding: 10px 20px;
  justify-self: center;
}
</style>
