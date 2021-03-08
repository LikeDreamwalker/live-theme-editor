<template>
  <div :class="$vuetify.breakpoint.mdAndUp ? 'preview-zone-overflow' : ''">
    <v-container>
      <!-- app -->
      <v-card
        :max-width="$vuetify.breakpoint.mdAndUp ? '50vw' : '100vw'"
        class="mx-auto mb-6"
      >
        <v-app-bar color="primary" dark>
          <v-app-bar-nav-icon></v-app-bar-nav-icon>

          <v-toolbar-title>镜湖 - MirrorLake</v-toolbar-title>

          <v-spacer></v-spacer>

          <v-btn icon>
            <v-icon>mdi-magnify</v-icon>
          </v-btn>
        </v-app-bar>

        <v-container>
          <v-row dense>
            <v-col cols="12">
              <v-card color="secondary" dark>
                <v-card-title class="headline"> 镜湖主题编辑器 </v-card-title>

                <v-card-subtitle>
                  在调色板选取颜色，点击颜色按钮即可部署<br />
                  你要是把这个app当调色板用我也说不了什么
                </v-card-subtitle>

                <v-card-actions>
                  <v-btn
                    text
                    href="https://github.com/LikeDreamwalker/mirrorlake-theme-editor"
                    >访问 github 以了解更多内容</v-btn
                  >
                </v-card-actions>
              </v-card>
            </v-col>

            <v-col cols="12">
              <v-card color="primary" dark>
                <div class="d-flex flex-no-wrap justify-space-between">
                  <div>
                    <v-card-title class="headline">
                      谁是LikeDreamwalker？
                    </v-card-title>
                    <v-card-subtitle>
                      “精通面向搜索引擎编程，了不起的前端CV开发工程师”
                    </v-card-subtitle>
                    <v-card-actions>
                      <v-btn text href="https://ldwid.com">
                        访问 ldwid.com 以了解更多内容
                      </v-btn>
                    </v-card-actions>
                  </div>

                  <v-avatar class="ma-3" size="125" tile>
                    <v-img
                      src="https://ldwid-1258491808.file.myqcloud.com/ldwid.com/LNOE_album.jpg/50p"
                    ></v-img>
                  </v-avatar>
                </div>
              </v-card>
            </v-col>

            <v-col v-for="(item, i) in items" :key="i" cols="12">
              <v-card :color="item.color" dark>
                <div class="d-flex flex-no-wrap justify-space-between">
                  <div>
                    <v-card-title
                      class="headline"
                      v-text="item.title"
                    ></v-card-title>

                    <v-card-subtitle v-text="item.artist"></v-card-subtitle>
                  </div>

                  <v-avatar class="ma-3" size="125" tile>
                    <v-img :src="item.src"></v-img>
                  </v-avatar>
                </div>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-card>
      <!-- alert -->
      <v-row>
        <v-col cols="12">
          <v-alert type="success" elevation="4"> I'm a success alert. </v-alert>
        </v-col>
        <v-col cols="12">
          <v-alert type="info" elevation="4"> I'm an info alert. </v-alert>
        </v-col>
        <v-col cols="12">
          <v-alert type="warning" elevation="4"> I'm a warning alert. </v-alert>
        </v-col>
        <v-col cols="12">
          <v-alert type="error" elevation="4"> I'm an error alert. </v-alert>
        </v-col>
      </v-row>
      <!-- button -->
      <v-row align="center">
        <v-col cols="12" sm="6">
          <div class="text-center">
            <div class="my-2">
              <v-btn x-small color="secondary">Extra small Button</v-btn>
            </div>
            <div class="my-2">
              <v-btn small color="primary">Small Button</v-btn>
            </div>
            <div class="my-2">
              <v-btn color="warning">Normal Button</v-btn>
            </div>
            <div class="my-2">
              <v-btn color="error" large>Large Button</v-btn>
            </div>
            <div class="my-2">
              <v-btn x-large color="success">Extra large Button</v-btn>
            </div>
          </div>
        </v-col>
        <v-col cols="12" sm="6">
          <div class="text-center">
            <div class="my-2">
              <v-btn color="secondary" fab x-small>
                <v-icon>mdi-television</v-icon>
              </v-btn>
            </div>
            <div class="my-2">
              <v-btn color="primary" fab small>
                <v-icon>mdi-pencil</v-icon>
              </v-btn>
            </div>
            <div class="my-2">
              <v-btn color="warning" fab>
                <v-icon>mdi-account-circle</v-icon>
              </v-btn>
            </div>
            <div class="my-2">
              <v-btn color="error" fab large>
                <v-icon>mdi-alarm</v-icon>
              </v-btn>
            </div>
            <div class="my-2">
              <v-btn color="success" fab x-large>
                <v-icon>mdi-domain</v-icon>
              </v-btn>
            </div>
          </div>
        </v-col>
      </v-row>
      <!-- chips -->
      <v-row align="center">
        <v-col
          v-for="item in themes"
          :key="item.name"
          :cols="$vuetify.breakpoint.mdAndUp ? 2 : 3"
        >
          <v-chip class="ma-2" :color="item.name">
            {{ item.name }}
          </v-chip>
        </v-col>
      </v-row>
      <!-- icon -->
      <v-row justify="space-around">
        <v-icon large color="primary">mdi-domain</v-icon>

        <v-icon large color="warning">mdi-message-text</v-icon>

        <v-icon large color="accent">mdi-dialpad</v-icon>

        <v-icon large color="error">mdi-email</v-icon>

        <v-icon large color="info">mdi-call-split</v-icon>

        <v-icon large color="success"> mdi-arrow-up-bold-box-outline </v-icon>
      </v-row>
      <div class="text-center mt-8">
        <div>
          <v-btn class="ma-2" color="primary" dark
            >Accept
            <v-icon dark right>mdi-checkbox-marked-circle</v-icon>
          </v-btn>

          <v-btn class="ma-2" color="error" dark
            >Decline
            <v-icon dark right>mdi-cancel</v-icon>
          </v-btn>

          <v-btn class="ma-2" color="secondary" dark>
            <v-icon dark left>mdi-minus_circle</v-icon>Cancel
          </v-btn>
        </div>

        <div>
          <v-btn class="ma-2" color="warning" dark>
            <v-icon dark left>mdi-arrow-left</v-icon>Back
          </v-btn>

          <v-btn class="ma-2" color="info" dark>
            <v-icon dark>mdi-wrench</v-icon>
          </v-btn>

          <v-btn class="ma-2" color="accent" dark>
            <v-icon dark>mdi-cloud-upload</v-icon>
          </v-btn>
        </div>

        <div>
          <v-btn class="ma-2" text icon color="success lighten-2">
            <v-icon>mdi-thumb-up</v-icon>
          </v-btn>

          <v-btn class="ma-2" text icon color="error lighten-2">
            <v-icon>mdi-thumb-down</v-icon>
          </v-btn>
        </div>
      </div>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          color: "info",
          src:
            "https://ldwid-1258491808.file.myqcloud.com/ldwid.com/Gallery/FSTO_blue_2020R.jpg/50p",
          title: "关于镜湖",
          artist:
            "MirrorLake 是 vuetify-theme-editor 的重构版本，免费并开放源码"
        },
        {
          color: "accent",
          src:
            "https://ldwid-1258491808.file.myqcloud.com/ldwid.com/DearJane_Remix.jpg/50p",
          title: "Dear Jane",
          artist: "LikeDreamwalker"
        }
      ],
      themes: [
        {
          name: "primary"
        },
        {
          name: "secondary"
        },
        {
          name: "accent"
        },
        {
          name: "error"
        },
        {
          name: "info"
        },
        {
          name: "success"
        },
        {
          name: "warning"
        }
      ]
    };
  }
};
</script>

<style lang="scss" scoped>
.preview-zone-overflow {
  overflow-y: auto;
  height: 100vh;
}
</style>