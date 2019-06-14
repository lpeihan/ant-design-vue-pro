<template>
  <div class="header-search">
    <a-icon type="search" @click.stop="enterSearchMode" />

    <a-auto-complete
      ref="autoComplete"
      :class="{ show: searchMode }"
      :dataSource="dataSource"
      placeholder="search"
      :filterOption="filterOption"
      @blur="blur"
      @change="handleChange"
      v-model="value"
    >
    </a-auto-complete>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dataSource: ["Burns Bay Road", "Downing Street", "Wall Street"],
      searchMode: false,
      value: ""
    };
  },
  methods: {
    // 不区分大小写
    filterOption(input, option) {
      return (
        option.componentOptions.children[0].text
          .toUpperCase()
          .indexOf(input.toUpperCase()) >= 0
      );
    },
    enterSearchMode() {
      this.searchMode = true;
      this.$refs.autoComplete.focus();
    },
    blur() {
      this.searchMode = false;
      this.value = "";
    },
    handleChange(val) {
      console.log(val);
    }
  }
};
</script>

<style lang="less" scoped>
.header-search {
  display: inline-block;
  padding: 0 12px;
  cursor: pointer;

  svg {
    width: 16px;
    height: 16px;
  }

  /deep/ .ant-select-search {
    width: 0;
    transition: width 0.3s;
    overflow: hidden;

    .ant-input {
      border: none;
      border-radius: 0;
      border-bottom: 1px solid @border-color-base;
    }
  }

  .show {
    /deep/ .ant-select-search {
      width: 210px;
    }
  }
}
</style>
