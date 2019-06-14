<template>
  <div class="header">
    <header-search></header-search>
    <notice-icon-view />
    <a-dropdown>
      <span class="header-global-dropdown">
        <a-icon type="global" />
      </span>
      <a-menu
        slot="overlay"
        @click="localeChange"
        :selectedKeys="[$route.query.locale || 'zhCN']"
      >
        <a-menu-item key="zhCN">
          中文
        </a-menu-item>
        <a-menu-item key="enUS">
          English
        </a-menu-item>
      </a-menu>
    </a-dropdown>
  </div>
</template>

<script>
import NoticeIconView from "@/components/GlobalHeader/NoticeIconView";
import HeaderSearch from "@/components/HeaderSearch";

export default {
  components: {
    NoticeIconView,
    HeaderSearch
  },
  methods: {
    localeChange({ key }) {
      this.$router.push({ query: { ...this.$route.query, locale: key } });
      this.$i18n.locale = key;
    }
  }
};
</script>

<style scoped lang="less">
.header {
  float: right;
  height: 100%;
  overflow: hidden;
  line-height: 64px;

  .header-global-dropdown {
    padding: 0 12px;
    display: inline-block;
    cursor: pointer;

    &:hover {
      background: @primary-1;
    }

    svg {
      width: 16px;
      height: 16px;
    }
  }
}
</style>
