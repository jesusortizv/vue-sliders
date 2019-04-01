<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <transition name="fade" mode="out-in">
          <v-btn v-if="!cookiesAccepted" @click="setPolicy()" color="info"
            >Cookies</v-btn
          >
        </transition>
      </v-toolbar-title>
      {{ queryParams }}
      <v-spacer></v-spacer>
      <div v-if="!isLogged">
        <span class="font-weight-medium">Ya eres un usuario?</span>
        <v-btn color="info">Inicio de sesion</v-btn>
      </div>
      <div v-else>
        <span class="font-weight-medium">Hola, Jesus Ortiz</span>
      </div>
    </v-toolbar>

    <v-content>
      <areas />
    </v-content>
  </v-app>
</template>

<script>
import Areas from "@/components/Areas";

export default {
  name: "App",
  components: {
    Areas
  },
  data() {
    return {
      cookiesAccepted: false,
      queryParams: {}
    };
  },
  computed: {
    isLogged() {
      return Object.keys(this.queryParams).some(key => {
        return key === "logged" && JSON.parse(this.queryParams[key]);
      });
    }
  },
  created() {
    this.cookiesAccepted = this.parseCookiesPolicy();
    this.queryParams = this.$route.query;
  },
  methods: {
    setPolicy() {
      localStorage.setItem("myCookies", "true");
      this.cookiesAccepted = this.parseCookiesPolicy();
    },
    parseCookiesPolicy() {
      return JSON.parse(localStorage.getItem("myCookies"));
    }
  }
};
</script>
