<template>
  <div>
    <b-navbar toggleable="lg" type="dark" sticky variant="dark">
      <b-container>
        <b-navbar-brand to="/">
          <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" class="d-inline-block align-top" viewBox="0 0 192.13 196.72"><g><g><path d="M166.87 100.62a71.54 71.54 0 0 1-70.81 70.8c-38.86.33-70.48-32.43-70.8-70.8-.14-16.28-25.4-16.3-25.26 0a98 98 0 0 0 26.75 66.51c16.88 18 40.66 28 65.06 29.44 24.86 1.46 49.1-8 67.83-24s29.43-39.31 32.07-63.53c.3-2.8.39-5.63.42-8.44.13-16.3-25.12-16.28-25.26 0z" fill="#4a5699"></path><path d="M25.26 96.07a71.54 71.54 0 0 1 70.8-70.81c16.28-.14 16.3-25.4 0-25.26a97.79 97.79 0 0 0-67.45 27.67C10.25 45.46.21 70.65 0 96.07c-.14 16.29 25.12 16.27 25.26 0z" fill="#c45fa0"></path><path d="M73.83 118.81c-10.58-14.11-9-30.09 4.14-41.46 12.31-10.62 30.52-6.6 40.93 6.34 4.33 5.37 13.39 4.48 17.86 0 5.26-5.25 4.31-12.5 0-17.86-17.42-21.65-50.71-25.9-73-9.21C40.58 74 34.26 107.87 52 131.56c4.12 5.5 10.82 8.31 17.28 4.53 5.42-3.18 8.66-11.76 4.53-17.28z" fill="#e5594f"></path><path d="M118.3 82.91c6 8 7.54 14 6.68 23.29.14-1.14.08-.93-.18.62-.26 1.32-.64 2.62-1 3.91a14.07 14.07 0 0 1-1.9 4.44c-2.34 4.43-4.59 6.68-8.84 10.1-5.38 4.32-4.48 13.39 0 17.86 5.25 5.26 12.5 4.31 17.85 0 21.66-17.42 25.91-50.71 9.22-73-4.12-5.5-10.82-8.31-17.28-4.53-5.43 3.18-8.67 11.76-4.53 17.28z" fill="#f39a2b"></path></g></g></svg>
          {{ $t(brandTitle) }}
        </b-navbar-brand>
        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <b-nav-item v-for="menu in menus" :to="menu.path" :key="menu.name" active-class="active">
              {{ $t(menu.name) }}
              <b-badge :variant="menu.variant" v-if="onMetric[menu.badge]"> {{ onMetric[menu.badge] }}</b-badge>
            </b-nav-item>
          </b-navbar-nav>
        </b-collapse>

        <b-navbar-nav class="ml-auto ">
          <b-nav-item>
            <b-dropdown size="sm" id="dlLang" text="secondary" variant="secondary" :text="$t('LanguageName')">
              <b-dropdown-item  v-for="lang in languages" class="text-secondary drop-active" :key="lang.code"
                :active="checkCurrentLang(lang.code)" @click="changeLang(lang.code)">{{ lang.name }}</b-dropdown-item>
            </b-dropdown>
          </b-nav-item>

          <b-nav-item href="https://github.com/dotnetcore/CAP" target="_blank" title="Github">
            <b-icon-github style="width:24px;height:24px"></b-icon-github>
          </b-nav-item>
        </b-navbar-nav>
      </b-container>
    </b-navbar>
  </div>
</template>
<script>
import { BIconGithub } from 'bootstrap-vue';
export default {
  name: "Navigation",
  components: {
    BIconGithub
  },
  computed: {
    onMetric() {
      return this.$store.getters.getMetric;
    }
  },
  methods: {
    changeLang(langCode) {
      localStorage.setItem('lang', langCode);
      this.$i18n.locale = langCode;
    },
    checkCurrentLang(langCode) {
      return this.$i18n.locale == langCode;
    }
  },
  data() {
    return {
      i18nPrefix: "_.Navigation.",
      brandTitle: "CAP Dashboard",
      languages: [
        { name: "English", code: "en-us", active: true },
        { name: "简体中文", code: "zh-cn", active: false }
      ],
      menus: [
        { name: "Published", path: "/published", variant: "danger", badge: "publishedFailed" },
        { name: "Received", path: "/received", variant: "danger", badge: "receivedFailed" },
        { name: "Subscriber", path: "/subscriber", variant: "info", badge: "subscribers" },
        { name: "Nodes", path: "/nodes", variant: "light", badge: "servers" },
      ]
    };
  },

};
</script>
<style scoped>
.nav-item {
  padding: 0 10px;
}

</style>
<style>
.drop-active .active{
 background-color: black !important;
}
</style>