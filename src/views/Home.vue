<template>
  <v-container fill-height fluid>
    <div class="d-flex container flex-column">
      <v-row class="text-center d-flex justify-center align-center">
        <v-col class="col-6">
          <who-am-i />
        </v-col>
      </v-row>
      <v-row class="d-flex justify-center align-center">
        <v-col class="col-6">
          <bash-top-layout>
            <template v-slot:title>
              What do I do ?
            </template>
            <template v-slot:body>
              <ul>
                <li>I do lines of codes...</li>
                <li>Cook and Eat comfy food</li>
                <li>Play games</li>
                <li>Party</li>
              </ul>
            </template>
          </bash-top-layout>
        </v-col>
      </v-row>
      <v-row class="d-flex justify-center align-center">
        <v-col class="col-6">
          <routing-command-line/>
        </v-col>
      </v-row>
    </div>
  </v-container>
</template>

<script>
import WhoAmI from "@/components/WhoAmI";
import BashTopLayout from "@/layouts/BashTopLayout";
import RoutingCommandLine from "@/components/RoutingCommandLine";

export default {
  name: "Home",
  components: { RoutingCommandLine, BashTopLayout, WhoAmI },
  mounted() {
    this.$refs.commandLineInput.focus();
  }
};
</script>

<style>
.hidden {
  opacity: 0;
}
</style>
