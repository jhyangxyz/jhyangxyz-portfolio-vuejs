<template>
  <v-container fill-height fluid>
    <v-row class="text-center d-flex align-center">
      <v-col>
        <div class="console-container">
          <span id="text"></span>
          <div class="console-underscore" id="console">&#95;</div>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
// @ is an alias to /src

// function([string1, string2],target id,[color1,color2])

function consoleText(words, id) {
  var visible = true;
  var con = document.getElementById("console");
  var letterCount = 1;
  var x = 1;
  var waiting = false;
  var target = document.getElementById(id);
  window.setInterval(function() {
    if (letterCount === 0 && waiting === false) {
      waiting = true;
      target.innerHTML = words[0].substring(0, letterCount);
      window.setTimeout(function() {
        var usedWord = words.shift();
        words.push(usedWord);
        x = 1;
        letterCount += x;
        waiting = false;
      }, 1000);
    } else if (letterCount === words[0].length + 1 && waiting === false) {
      waiting = true;
      window.setTimeout(function() {
        x = -1;
        letterCount += x;
        waiting = false;
      }, 1000);
    } else if (waiting === false) {
      target.innerHTML = words[0].substring(0, letterCount);
      letterCount += x;
    }
  }, 120);
  window.setInterval(function() {
    if (visible === true) {
      con.className = "console-underscore hidden";
      visible = false;
    } else {
      con.className = "console-underscore";

      visible = true;
    }
  }, 400);
}

export default {
  name: "Home",
  mounted() {
    consoleText(
      [
        "I'm Jeong-Heon YANG\n",
        "Je suis Jeong-Heon YANG",
        "Ich bin Jeong-Heon YANG",
        "양정헌입니다"
      ],
      "text"
    );
  }
};
</script>

<style>
.console-underscore {
  display: inline-block;
  position: relative;
  top: 0;
  left: 4px;
}

.hidden {
  opacity: 0;
}
</style>
