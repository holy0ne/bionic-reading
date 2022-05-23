<template>
  <v-app>
    <v-app-bar
      id="Header"
      class="pa-0"
      color="white"
      app
      clipped-right
      extension-height="100"
      elevation="0"
    >
      <v-toolbar color="transparent" flat>
        <v-toolbar-title>
          <img src="/icon.png" style="max-width: 20px" />
          <strong>BIO</strong>NIC.<strong>O</strong>NE
        </v-toolbar-title>

        <v-spacer></v-spacer>

        <v-btn
          color="black"
          href="https://github.com/holy0ne/bionic-reading"
          icon
        >
          <v-icon>mdi-github</v-icon>
        </v-btn>
      </v-toolbar>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed" app color="white">
      <v-row class="align-center mx-0 mb-2 box">
        <v-col cols="12" sm="auto">
          <span>
            &copy; {{ new Date().getFullYear() }} -
            <strong>bionic.one</strong>
          </span>
        </v-col>
        <v-spacer />
        <v-col cols="12" sm="auto">
          Donate some NANO 😇 :
          <strong>
            nano_15heno99oc5m5zwgyacxm5m5o1ia9maxme9w5prhk18sakwnt464zjh9io5m
          </strong>
        </v-col>
      </v-row>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "DefaultLayout",
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: "mdi-apps",
          title: "Welcome",
          to: "/",
        },
        {
          icon: "mdi-chart-bubble",
          title: "Inspire",
          to: "/inspire",
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: "Vuetify.js",
    };
  },
};
</script>

<style lang="scss">
@import "~/assets/variables.scss";

::-moz-selection {
  /* Code for Firefox */
  color: lighten($primary, 10);
  background: black;
}

::selection {
  color: lighten($primary, 10);
  background: black;
}

.box {
  background-color: lighten($primary, 15);
  border-radius: 8px;
  strong {
    max-width: 100%;
    word-break: break-all;
  }
}
</style>
