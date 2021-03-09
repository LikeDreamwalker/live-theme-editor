# mirrorlake-theme-editor

### 镜湖主题编辑器

Demo: https://lte.ldwid.com

#### 关于镜湖

MirrorLake 是 vuetify-theme-editor 的重构版本，在基于VTE的基础上进行了多个修复和改进，并且加入了很多新功能，目前已经较为完善：

- 支持RGB，HSL以及HEX颜色
- 全局主题颜色实时更改
- 将配置好的主题保存为.json文件以供使用
- 支持夜间模式
- 完全开源

vuetify有原生的主题编辑器，但是作为主题编辑器，其只提供了少量的颜色以及简单的预览效果，这无法满足部分用户的需求。在此基础上， vuetify-theme-editor 诞生了（ https://github.com/LikeDreamwalker/vuetify-theme-editor ）。但VTE并不是一个完美的框架，依然欠缺了部分核心的功能，同时面临一定的性能问题。

在此基础上，我重构了VTE，并使用 MirrorLake 作为重构策略，重新设置了这个应用，以符合更多人的使用方式。

#### 如何使用

镜湖非常容易上手。

镜湖的核心是一个颜色选择器，所以你只需要选择你想要的颜色，再点击你想要将颜色部署的按钮（例如primary）即可成功部署，此时主题色primary就会发生对应的变化，而其他相关组件也会发生变化，以供预览。

#### Roadmap

镜湖目前依然受限于vuetify以及MD，这是无法避免的问题。

所以在下一个版本中，镜湖会加入添加额外的主题色（类似SASS变量），并由用户决定将主题色部署在哪些示例组件上。这在技术上没有什么难度，但是在设计层面上很有挑战。我又不是设计师。

#### 我想要使用源码

在协议的限制下使用源码。如果你想要在本地启动这个程序，需要执行

`npm install`

 `npm run serve`

#### 我有更好的想法

我非常需要一些新的想法来帮助我完成镜湖的迭代。你可以open issue或者给我发邮件。

#### 技术栈

镜湖基于 Vue2 以及 Vuetify 开发，代码托管于 Github ，部署于 Vercel，静态资源于云服务依赖于腾讯云。

#### For English Version

Not like VTE, I have already been tired of writing different version readmes and startups. But I think you can still use this app directly.

Also, just open a issue or connect me as you need.
