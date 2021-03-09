<template>
  <div
    :width="$vuetify.breakpoint.mdAndUp ? '50vw' : '100vw'"
    :max-width="$vuetify.breakpoint.mdAndUp ? '50vw' : '100vw'"
  >
    <!-- 取色器 -->
    <v-color-picker
      :canvas-height="
        $vuetify.breakpoint.mdAndUp ? getHeight(0.3, 0.4) : getHeight(0.3, 0.4)
      "
      :width="
        $vuetify.breakpoint.mdAndUp ? getWidth(1, 0.49) : getWidth(1, 0.5)
      "
      :hide-canvas="!colorPickerStatus[0].status"
      :hide-inputs="!colorPickerStatus[1].status"
      :show-swatches="colorPickerStatus[2].status"
      :disabled="colorPickerStatus[3].status"
      :swatches-max-height="
        $vuetify.breakpoint.mdAndUp
          ? getSwatchesHeight(0.2, 0.2)
          : getSwatchesHeight(0.2, 0.2)
      "
      v-model="color"
    >
    </v-color-picker>

    <!-- 操作组 -->
    <v-container>
      <v-row>
        <v-col
          v-for="item in colorPickerStatus"
          :key="item.name"
          class="d-flex justify-center"
          :cols="$vuetify.breakpoint.mdAndUp ? 3 : 4"
        >
          <v-btn
            :color="item.status ? color : ''"
            @click="item.status = !item.status"
            rounded
            x-large
            :width="$vuetify.breakpoint.mdAndUp ? '10vw' : '32vw'"
          >
            <div class="text--button flex-grow-1 text-center">
              <span
                v-if="item.lock"
                class="mdi"
                :class="item.status ? 'mdi-lock' : 'mdi-lock-open'"
              >
              </span>
              <span
                v-if="item.check"
                class="mdi"
                :class="item.status ? 'mdi-check' : 'mdi-close'"
              >
              </span>
              {{ item.name }}
            </div>
          </v-btn>
        </v-col>
        <v-col
          :cols="$vuetify.breakpoint.mdAndUp ? 3 : 4"
          class="d-flex justify-center"
        >
          <v-btn
            class="d-flex align-center"
            @click="setDark()"
            rounded
            x-large
            :width="$vuetify.breakpoint.mdAndUp ? '10vw' : '32vw'"
          >
            <div class="text--button flex-grow-1 text-center">
              <span
                class="mdi"
                :class="
                  $vuetify.theme.dark ? 'mdi-brightness-4' : 'mdi-brightness-7'
                "
              ></span>
              {{ this.$vuetify.theme.dark ? "夜间" : "日间" }}
            </div>
          </v-btn>
        </v-col>
        <v-col
          :cols="$vuetify.breakpoint.mdAndUp ? 3 : 4"
          class="d-flex justify-center"
        >
          <v-btn
            class="d-flex align-center"
            @click="openDialog()"
            :color="color"
            rounded
            x-large
            :width="$vuetify.breakpoint.mdAndUp ? '10vw' : '32vw'"
          >
            <div class="text--button flex-grow-1 text-center">
              <span class="mdi mdi-backup-restore"></span>
              默认主题
            </div>
          </v-btn>
        </v-col>
      </v-row>
    </v-container>

    <!-- 按钮组 -->
    <v-container>
      <v-row>
        <v-col
          :cols="$vuetify.breakpoint.mdAndUp ? 3 : 4"
          v-for="item in themes"
          :key="item.name"
          class="d-flex justify-center"
        >
          <v-btn
            rounded
            x-large
            :width="$vuetify.breakpoint.mdAndUp ? '10vw' : '32vw'"
            :color="item.name"
            @click="setColor(item.name)"
            :disabled="colorPickerStatus[3].status"
          >
            <div class="text--button flex-grow-1 text-center">
              {{ item.name }}
              <br />
              {{
                $vuetify.theme.dark === true
                  ? $vuetify.theme.themes.dark[item.name]
                  : $vuetify.theme.themes.light[item.name]
              }}
            </div>
          </v-btn>
        </v-col>
        <v-col
          :cols="$vuetify.breakpoint.mdAndUp ? 3 : 4"
          class="d-flex justify-center"
        >
          <v-btn
            class="d-flex align-center"
            @click="codeDialog = true"
            color="#00bbff"
            rounded
            x-large
            :width="$vuetify.breakpoint.mdAndUp ? '10vw' : '32vw'"
          >
            <div class="text--button flex-grow-1 text-center">
              <span class="mdi mdi-download"></span>
              保存
            </div>
          </v-btn>
        </v-col>
      </v-row>
    </v-container>

    <!-- dialog -->
    <v-dialog
      v-model="dialog"
      :max-width="$vuetify.breakpoint.mdAndUp ? '20vw' : '80vw'"
    >
      <v-card>
        <v-card-title class="headline">恢复预置主题</v-card-title>

        <v-card-text>
          你想要将<b>{{
            this.$vuetify.theme.dark === true ? "夜间主题" : "日间主题"
          }}</b
          >恢复为预置主题吗？所有设置均不会保存
        </v-card-text>

        <v-card-actions>
          <v-spacer></v-spacer>

          <v-btn color="#0066FF" text @click="dialog = false"> 我再想想 </v-btn>

          <v-btn
            color="#0066FF"
            text
            @click="
              dialog = false;
              setDefaultTheme();
            "
          >
            好的
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-dialog
      v-model="codeDialog"
      :max-width="$vuetify.breakpoint.mdAndUp ? '20vw' : '80vw'"
    >
      <v-card>
        <v-card-title class="headline">保存为.json文件</v-card-title>

        <v-card-text>
          主题配置代码将被保存为一个名为<b>MirrorLake_时间戳</b>的.json文件，请勿拦截下载
        </v-card-text>

        <v-card-actions>
          <v-spacer></v-spacer>

          <v-btn color="#0066FF" text @click="codeDialog = false">
            我再想想
          </v-btn>

          <v-btn
            color="#0066FF"
            text
            @click="
              codeDialog = false;
              saveJSON();
            "
          >
            好的
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import dayjs from "dayjs";
export default {
  data() {
    return {
      fHeight: null,
      fWidth: null,
      sHeight: null,
      portraitHeight: null,
      landscapeHeight: null,
      portraitWidth: null,
      landscapeWidth: null,
      swatchesPortraitHeight: null,
      swatchesLandscapeHeight: null,
      colorPickerStatus: [
        { status: true, check: true, name: "画板" },
        { status: true, check: true, name: "输入" },
        { status: false, check: true, name: "色板" },
        { status: false, lock: true, name: "禁用" }
      ],
      test: true,
      color: "#0066FFFF",
      dialog: false,
      codeDialog: false,
      confirm: false,

      themes: [
        {
          name: "primary",
          light: "#1976D2",
          dark: "#2196F3"
        },
        {
          name: "secondary",
          light: "#424242",
          dark: "#424242"
        },
        {
          name: "accent",
          light: "#82B1FF",
          dark: "#FF4081"
        },
        {
          name: "error",
          light: "#FF5252",
          dark: "#FF5252"
        },
        {
          name: "info",
          light: "#2196F3",
          dark: "#2196F3"
        },
        {
          name: "success",
          light: "#4CAF50",
          dark: "#4CAF50"
        },
        {
          name: "warning",
          light: "#FB8C00",
          dark: "#FB8C00"
        }
      ]
    };
  },
  methods: {
    // 默认匹配竖屏
    getHeight(portraitHeight, landscapeHeight) {
      let mql = window.matchMedia("(orientation: portrait)");
      let _this = this;
      // 赋予默认高度
      computeHeight(portraitHeight, landscapeHeight, mql);
      mql.addListener(handleOrientationChange);
      return this.fHeight;
      // 监听

      function handleOrientationChange(mql) {
        computeHeight(portraitHeight, landscapeHeight, mql);
      }
      // 计算高度
      function computeHeight(portraitHeight, landscapeHeight, mql) {
        if (mql.matches) {
          _this.fHeight = window.innerHeight * portraitHeight;
        } else {
          _this.fHeight = window.innerHeight * landscapeHeight;
        }
      }
    },

    getWidth(portraitWidth, landscapeWidth) {
      let mql = window.matchMedia("(orientation: portrait)");
      let _this = this;
      // 赋予默认宽度
      computeWidth(portraitWidth, landscapeWidth, mql);
      mql.addListener(handleOrientationChange);
      return this.fWidth;
      // 监听

      function handleOrientationChange(mql) {
        computeWidth(portraitWidth, landscapeWidth, mql);
      }
      // 计算宽度
      function computeWidth(portraitWidth, landscapeWidth, mql) {
        if (mql.matches) {
          _this.fWidth = window.innerWidth * portraitWidth;
        } else {
          _this.fWidth = window.innerWidth * landscapeWidth;
        }
      }
    },

    getSwatchesHeight(swatchesPortraitHeight, swatchesLandscapeHeight) {
      let mql = window.matchMedia("(orientation: portrait)");
      let _this = this;
      // 赋予默认高度
      computeHeight(swatchesPortraitHeight, swatchesLandscapeHeight, mql);
      mql.addListener(handleOrientationChange);
      return this.sHeight;
      // 监听

      function handleOrientationChange(mql) {
        computeHeight(swatchesPortraitHeight, swatchesLandscapeHeight, mql);
      }
      // 计算高度
      function computeHeight(
        swatchesPortraitHeight,
        swatchesLandscapeHeight,
        mql
      ) {
        if (mql.matches) {
          _this.sHeight = window.screen.height * swatchesPortraitHeight;
        } else {
          _this.sHeight = window.screen.height * swatchesLandscapeHeight;
        }
      }
    },

    setColor(buttonName) {
      const name = buttonName;
      const realColor = this.color.substring(0, 7);
      if (this.$vuetify.theme.dark === true) {
        this.$vuetify.theme.themes.dark[name] = realColor;
      } else {
        this.$vuetify.theme.themes.light[name] = realColor;
      }
    },

    setDark() {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    },

    setDefaultTheme() {
      this.themes.forEach((element) => {
        if (this.$vuetify.theme.dark === true) {
          this.$vuetify.theme.themes.dark[element.name] = element.dark;
        } else {
          this.$vuetify.theme.themes.light[element.name] = element.light;
        }
      });
      this.color = "#0066FFFF";
    },

    openDialog() {
      this.dialog = true;
    },

    saveJSON() {
      let data = this.$vuetify.theme.themes;
      data = JSON.stringify(data, undefined, 4);
      let blob = new Blob([data], { type: "text/json" }),
        e = document.createEvent("MouseEvents"),
        a = document.createElement("a");
      a.download = `MirrorLake-${dayjs().format("YYYY-MM-DD-HH-mm-ss")}.json`;
      a.href = window.URL.createObjectURL(blob);
      a.dataset.downloadurl = ["text/json", a.download, a.href].join(":");
      e.initMouseEvent(
        "click",
        true,
        false,
        window,
        0,
        0,
        0,
        0,
        0,
        false,
        false,
        false,
        false,
        0,
        null
      );
      a.dispatchEvent(e);
    }
  },
  created() {}
};
</script>

<style lang="scss">
</style>