<template>
  <div class="layout-wrapper">
    <Layout class="layout-outer">
      <Sider
        :width="300"
        collapsible
        hide-trigger
        reverse-arrow
        v-model="collapsed"
      >
        <side-menu
          :collapsed="collapsed"
          :list="menuList"
        ></side-menu>
      </Sider>
      <Layout>
        <Header class="header-wrapper">
          <Icon
            :class="triggerClasses"
            @click.native="handleCollapsed"
            type="md-menu"
            :size="32"
          />
        </Header>
        <Content class="content-con">
          <Card
            shadow
            class="page-card"
          >
            <router-view />
          </Card>
        </Content>
      </Layout>
    </Layout>
  </div>
</template>

<script>
import SideMenu from "_c/SideMenu";
export default {
  components: {
    SideMenu
  },
  data() {
    return {
      collapsed: true,
      menuList: [
        {
          title: "1",
          name: "menu1",
          icon: "ios-alarm"
        },
        {
          title: "2",
          name: "menu2",
          icon: "ios-alarm",
          children: [
            {
              title: "2-1",
              name: "menu21",
              icon: "ios-alarm"
            },
            {
              title: "2-2",
              name: "menu22",
              icon: "ios-alarm"
            }
          ]
        },
        {
          title: "3",
          name: "menu3",
          icon: "ios-alarm",
          children: [
            {
              title: "3-1",
              name: "menu31",
              icon: "ios-alarm"
            },
            {
              title: "3-2",
              name: "menu32",
              icon: "ios-alarm",
              children: [
                {
                  title: "3-2-1",
                  name: "menu321",
                  icon: "ios-alarm"
                },
                {
                  title: "3-2-2",
                  name: "menu322",
                  icon: "ios-alarm",
                  children: [
                    {
                      title: "3-2-2-1",
                      name: "menu3221",
                      icon: "ios-alarm"
                    }
                  ]
                }
              ]
            }
          ]
        }
      ]
    };
  },
  computed: {
    triggerClasses() {
      return ["trigger-icon", this.collapsed ? "rotate" : ""];
    }
  },
  methods: {
    handleCollapsed() {
      this.collapsed = !this.collapsed;
    }
  }
};
</script>

<style lang="less" scope>
.layout-wrapper,
.layout-outer {
  height: 100%;
  .header-wrapper {
    background: #fff;
    box-shadow: 0 1px 1px 1px rgba(0, 0, 0, 0.1);
    padding: 0 23px;
    .trigger-icon {
      cursor: pointer;
      transition: transform 0.3s ease;
      &.rotate {
        transform: rotateZ(-90deg);
        transition: transform 0.3s ease;
      }
    }
  }
  .content-con {
    padding: 10px;
  }
  .page-card {
    min-height: ~"calc(100vh - 84px)";
  }
}
</style>
