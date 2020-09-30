<template>
  <v-container fill-height fluid>
    <v-row class="text-center d-flex align-center">
      <v-col>
        <div class="console-container">
          <div>
            <span id="vue-console-text">
              {{ showedText }}
            </span>
            <div
              class="console-underscore"
              :class="{ hidden: !consoleUnderscoreVisible }"
            >
              &#95;
            </div>
          </div>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
// @ is an alias to /src
import * as hangul from "hangul-js";

export default {
  name: "Home",
  data() {
    return {
      consoleText: "",
      consoleUnderscoreVisible: true,
      waiting: false,
      directionReversed: false,
      x: 0,
      words: [
        "양정헌입니다",
        "I'm Jeong-Heon YANG",
        "Je suis Jeong-Heon YANG"
      ],
      currentWord: "",
      isKorean: false
    };
  },
  computed: {
    letterCount() {
      return this.consoleText.length;
    },
    isWordFinished() {
      return (
        this.currentWord === "" ||
        (this.consoleText === "" && this.directionReversed)
      );
    },
    isWordReversable() {
      return (
        this.letterCount === this.currentWord.length &&
        this.waiting === false &&
        this.x >= this.currentWord.length
      );
    },
    showedText() {
      if (this.isKorean) {
        return hangul.assemble(this.consoleText);
      } else {
        return this.consoleText;
      }
    }
  },
  mounted() {
    window.setInterval(this.activateBotTyper, 120);
    window.setInterval(this.activateUnderscoreBlink, 400);
  },
  destroyed() {
    clearInterval(this.activateBotTyper);
    clearInterval(this.activateUnderscoreBlink);
  },
  methods: {
    activateUnderscoreBlink() {
      this.consoleUnderscoreVisible = !this.consoleUnderscoreVisible;
    },
    activateBotTyper() {
      if (this.waiting) {
        return;
      }
      if (this.isWordFinished) {
        this.waiting = true;
        let tmpWord = this.words.shift();
        let nextWord = "";

        if (
          tmpWord
            .charAt(0)
            .match(
              /[\uac00-\ud7af]|[\u1100-\u11ff]|[\u3130-\u318f]|[\ua960-\ua97f]|[\ud7b0-\ud7ff]/g
            ) !== null
        ) {
          this.isKorean = true;
          tmpWord = hangul.disassemble(tmpWord);

          tmpWord.forEach(char => {
            nextWord += char;
          });
        } else {
          nextWord = tmpWord;
          this.isKorean = false;
        }
        this.currentWord = nextWord;
        this.words.push(this.currentWord);
        this.reverseDirection();
      } else if (this.isWordReversable) {
        this.waiting = true;
        this.reverseDirection();
      } else {
        if (this.directionReversed) {
          this.consoleText = this.consoleText.slice(0, -1);
        } else {
          this.consoleText += this.currentWord.charAt(this.x);
        }
        this.x++;
      }
    },
    reverseDirection() {
      let savedDirection = this.directionReversed;
      window.setTimeout(() => {
        if (savedDirection === !this.directionReversed) {
          return;
        }
        this.x = 0;
        this.directionReversed = !this.directionReversed;
        this.waiting = false;
      }, 1000);
    }
  }
};
</script>

<style>
.console-underscore {
  display: inline-block;
  position: relative;
  top: 0;
  left: -6px;
}

.hidden {
  opacity: 0;
}
</style>
