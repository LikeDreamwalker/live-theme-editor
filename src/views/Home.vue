<template>
  <v-main>
    <v-title>
      vuetify-theme-editor
    </v-title>
    <v-row>
      <!-- color-picker -->
      <v-col cols="12" lg="4" md="4" sm="12" xl="4">
        <v-card elevation="0">
          <v-row align-content="start" justify="center">
            <v-col cols="2"></v-col>
            <v-col cols="8">
              <v-color-picker
                show-swatches
                :swatches-max-height="
                  $vuetify.breakpoint.mdAndUp ? '60vh' : '40vh'
                "
                width="300"
                elevation="12"
                class="rounded-xl"
                v-model="color"
                mode="rgba"
              ></v-color-picker>
            </v-col>
            <v-col cols="2"></v-col>
          </v-row>
        </v-card>
      </v-col>
      <!-- info&code -->
      <v-col cols="12" lg="4" md="4" sm="12" xl="4"
        ><v-card
          elevation="12"
          class="mx-5 my-2 rounded-xl overflow-y-auto overflow-x-hidden"
          :max-height="$vuetify.breakpoint.mdAndUp ? '90vh' : '60vh'"
        >
          <a href="https://www.ldwid.com">
            <v-img
              src="https://ldwid-1258491808.file.myqcloud.com/LDW_2020_ID_WEB.png"
            >
            </v-img>
          </a>
          <v-card-title style="word-break:break-word">
            Welcome to vuetify-theme-editor!
          </v-card-title>
          <v-card-subtitle style="word-break:break-word">
            Ver 1.00 LikeDreamwalker
          </v-card-subtitle>
          <v-card-text style="word-break:break-word">
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>How do I use this app?</v-list-item-title>
                <v-card-text>
                  You can use the color picker to select the color you want,
                  then click the button, the theme-color will be changed
                  automatically.The code will show below.
                </v-card-text>
                <v-list-item-title>Things you have to know:</v-list-item-title>
                <v-card-text>
                  <b>DO NOT USE ALPHA AND IT WON'T WORK.</b>
                  <br />
                  Though this app can work on mobile devices, for a better
                  experience you should rotate your screen or use PC.
                  <br />
                  For some unknow reasons, there might be a problem for Safari,
                  which I think it's not my fault :)
                </v-card-text>
              </v-list-item-content>
            </v-list-item>
            <v-divider></v-divider>
          </v-card-text>
          <v-row>
            <v-col
              v-for="theme in themes"
              v-bind:key="theme.name"
              :cols="$vuetify.breakpoint.smAndUp ? '4' : '6'"
              align-self="center"
            >
              <v-btn
                fab
                elevation="12"
                width="5rem"
                height="5rem"
                class="my-2 ml-7"
                :color="theme.name"
                :style="
                  $vuetify.breakpoint.mdAndUp
                    ? 'font-size:0.25rem'
                    : 'font-size:0.5rem'
                "
                @click="
                  theme.status = 1;
                  setColor(theme.name, theme.status);
                "
              >
                {{ theme.name }}
              </v-btn>
            </v-col>
          </v-row>
          <v-divider></v-divider>
          <v-row>
            <v-col cols="12">
              <v-card elevation="0">
                <v-card-text>
                  <pre style="font-family: sans-serif">
const vuetify = new Vuetify({
theme: {
  themes: {
    light: {
      primary: '{{ this.$vuetify.theme.themes.light.primary }}',
      secondary: '{{ this.$vuetify.theme.themes.light.secondary }}',
      accent: '{{ this.$vuetify.theme.themes.light.accent }}',
      error: '{{ this.$vuetify.theme.themes.light.error }}',
      info: '{{ this.$vuetify.theme.themes.light.info }}',
      success: '{{ this.$vuetify.theme.themes.light.success }}',
      warning: '{{ this.$vuetify.theme.themes.light.warning }}',
      },
    },
  },
})
                 </pre
                  >
                </v-card-text>
              </v-card>
            </v-col>
          </v-row>
          <v-row>
            <v-btn block color="warning" elevation="12" @click="setDefault()">
              set everything into normal!
            </v-btn>
          </v-row>
        </v-card>
      </v-col>
      <!-- preview-zone -->
      <v-col cols="12" lg="4" md="4" sm="12" xl="4">
        <v-card
          elevation="12"
          class="d-flex flex-wrap justify-space-around mx-5 my-2 rounded-xl overflow-y-auto overflow-x-hidden"
          :max-height="$vuetify.breakpoint.mdAndUp ? '90vh' : '60vh'"
        >
          <v-row>
            <v-col cols="1"> </v-col>
            <v-col cols="10">
              <!-- alerts -->
              <v-row>
                <v-col cols="12">ALERTS</v-col>
                <v-col v-for="theme in themes" v-bind:key="theme.name">
                  <v-alert
                    :color="theme.name"
                    width="100%"
                    min-width="250px"
                    elevation="12"
                  >
                    {{ theme.name }}
                  </v-alert>
                </v-col> </v-row
              ><v-divider></v-divider>
              <!-- chips -->
              <v-row>
                <v-col cols="12">CHIPS</v-col>
                <v-col v-for="theme in themes" v-bind:key="theme.name">
                  <v-chip :color="theme.name" width="5vw" min-width="50px">
                    {{ theme.name }}
                  </v-chip>
                </v-col> </v-row
              ><v-divider></v-divider>
              <!-- AVATARS -->
              <v-row>
                <v-col cols="12">AVATARS</v-col>
                <v-col v-for="theme in themes" v-bind:key="theme.name">
                  <v-avatar :color="theme.name" size="62">
                    {{ theme.name }}
                  </v-avatar>
                </v-col> </v-row
              ><v-divider></v-divider>
              <!-- Badges -->
              <v-row>
                <v-col cols="12">BADGES</v-col>
                <v-toolbar>
                  <v-tabs dark background-color="primary" grow>
                    <v-tab>
                      <v-badge color="info" dot>
                        Item One
                      </v-badge>
                    </v-tab>

                    <v-tab>
                      <v-badge color="success" content="6">
                        Item Two
                      </v-badge>
                    </v-tab>

                    <v-tab>
                      <v-badge color="warning" icon="mdi-vuetify">
                        Item Three
                      </v-badge>
                    </v-tab>
                  </v-tabs>
                </v-toolbar> </v-row
              ><v-divider></v-divider>
              <!-- Banners -->
              <v-row>
                <v-col cols="12">BANNERS</v-col>
                <v-banner two-line>
                  <v-avatar slot="icon" color="primary" size="40">
                    <v-icon icon="mdi-lock" color="white">
                      mdi-lock
                    </v-icon>
                  </v-avatar>
                  Hey！
                  <template v-slot:actions>
                    <v-btn text color="primary">Action</v-btn>
                    <v-btn text color="primary">Action</v-btn>
                  </template>
                </v-banner> </v-row
              ><v-divider></v-divider>
              <!-- Buttons -->
              <v-row>
                <v-col cols="12">BUTTONS</v-col>
                <v-col
                  v-for="theme in themes"
                  v-bind:key="theme.name"
                  :cols="$vuetify.breakpoint.smAndUp ? '4' : '6'"
                  align-self="center"
                >
                  <v-btn
                    elevation="12"
                    x-large
                    outlined
                    class="my-2 ml-7"
                    :color="theme.name"
                    :style="
                      $vuetify.breakpoint.mdAndUp
                        ? 'font-size:0.25rem'
                        : 'font-size:0.5rem'
                    "
                  >
                    {{ theme.name }}
                  </v-btn>
                </v-col>
              </v-row>
              <v-divider></v-divider>
              <v-row>
                <v-col cols="12">
                  THERE WILL BE SOMETHING MORE...
                </v-col>
              </v-row>
            </v-col>
            <v-col cols="1"> </v-col>
          </v-row> </v-card
      ></v-col>
    </v-row>
  </v-main>
</template>

<script>
import VTitle from "../components/title";
export default {
  data: () => ({
    themes: [
      {
        name: "primary",
        status: 0,
        default: "#1976D2"
      },
      {
        name: "secondary",
        status: 0,
        default: "#424242"
      },
      {
        name: "accent",
        status: 0,
        default: "#82B1FF"
      },
      {
        name: "error",
        status: 0,
        default: "#FF5252"
      },
      {
        name: "info",
        status: 0,
        default: "#2196F3"
      },
      {
        name: "success",
        status: 0,
        default: "#4CAF50"
      },
      {
        name: "warning",
        status: 0,
        default: "#FFC107"
      }
    ],
    color: "",
    code: "Copy code."
  }),
  methods: {
    setColor(buttonName, buttonStatus) {
      const name = buttonName;
      const status = buttonStatus;
      // get color like #0066ff not #0066ffaa
      // Vuetify theme doesn't support color with alpha
      const realColor = this.color.substring(0, 7);
      if (status == 1) {
        this.$vuetify.theme.themes.light[name] = realColor;
        this.themes.status = 0;
      } else {
        alert(
          "There is something wrong and that's not your fault. Please connect me."
        );
      }
    },
    setDefault() {
      const c = confirm(
        "Are you sure you want to set theme into default? All the codes won't be saved. "
      );
      if (c == true) {
        this.themes.forEach(element => {
          this.$vuetify.theme.themes.light[element.name] = element.default;
        });
      }
    }
  },
  components: {
    VTitle
  }
};
</script>

<style lang="scss">
#code {
  font-family: serif;
  font-size: 1.5rem;
  color: pink;
}
</style>
