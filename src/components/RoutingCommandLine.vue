<template>
  <bash-top-layout>
    <template v-slot:title>
      Looking for something ?
    </template>
    <template v-slot:body>
      <div class="commands-container">
        <span class="primary--text"><strong>Available Commands:</strong></span>
        <ul v-for="command in availableCommands" :key="command">
          <li>
            <div class="d-flex justify-space-between">
              <div>{{ command }}</div>
<!--              <div>Description</div>-->
            </div>
          </li>
        </ul>
        <template v-for="(historyCommand, index) in commandHistory">
          <span :key="index">{{ historyCommand }}<br /></span>
        </template>

        $<input
          type="text"
          class="secondary--text pl-3"
          ref="commandLineInput"
          placeholder="Enter a command"
          v-on:keyup.enter="onEnter"
          v-model="commandLineText"
        />
      </div>
    </template>
  </bash-top-layout>
</template>

<script>
import BashTopLayout from "@/layouts/BashTopLayout";

export default {
  name: "routing-command-line",
  components: { BashTopLayout },
  data() {
    return {
      commandLineText: "",
      availableCommands: [
        "portfolio",
        "contact",
        "github",
        "linkedin",
        "gitlab"
      ],
      commandHistory: []
    };
  },
  methods: {
    onEnter() {
      console.log("Entered");
      console.log(this.commandLineText);
      // console.log(this.availableCommands.includes('portfolio'));
      if (this.availableCommands.includes(this.commandLineText)) {
        switch (this.commandLineText) {
          case "portfolio":
          case "contact":
            this.commandHistory.push( '$ ' + this.commandLineText + " not available yet");
            break;
          case "github":
            window.location = "https://github.com/jhyangxyz";
            break;
          case "linkedin":
            window.location =
              "https://www.linkedin.com/in/jeong-heon-yang-625014a5/";
            break;
          case "gitlab":
            window.location = "https://gitlab.jhyang.xyz/jhyangxyz";
            break;
          default:
            this.commandHistory.push(
              "$ Unkown command: " + this.commandLineText
            );
            break;
        }
      } else {
        this.commandHistory.push("$ Unkown command: " + this.commandLineText);
      }

      this.commandLineText = "";
    }
  }
};
</script>

<style scoped>
.commands-container ul {
  list-style: none;
  padding-right: 24px;
}

.commands-container input {
  -webkit-appearance: none;
  background: none;
  border: 0;
  outline: 0;
  padding: 0;
}
</style>
