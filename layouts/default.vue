<template>
  <v-app dark>
    <!-- <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-list-item to="/">
          <v-list-item-action>
            <v-icon>mdi-apps</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Welcome</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-divider></v-divider>
      <v-layout column justify-center justify-space-between fill-height>
        <div>
          <v-list>
            <v-list-item
              v-for="(item, i) in items"
              :key="i"
              :to="item.to"
              router
              exact
            >
              <v-list-item-action>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-action>
              <v-list-item-content>
                <v-list-item-title v-text="item.title" />
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </div>
        <div>
          <v-divider></v-divider>
          <v-list>
            <v-list-item @click.stop="miniVariant = !miniVariant">
              <v-list-item-action>
                <v-icon
                  >mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon
                >
              </v-list-item-action>
              <v-list-item-content>
                <v-list-item-title>Minimize</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </div>
      </v-layout>
    </v-navigation-drawer> -->
    <!-- <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />

      <v-toolbar-title v-text="title" />
      <v-spacer />
      <v-btn icon @click.stop="rightDrawer = !rightDrawer">
        <v-icon>mdi-account</v-icon>
      </v-btn>
    </v-app-bar> -->
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-navigation-drawer v-model="rightDrawer" :right="right" temporary fixed>
      <v-list>
        <v-list-item>
          <v-list-item-action>
            <v-icon> mdi-account-edit </v-icon>
          </v-list-item-action>
          <v-list-item-title>My Profile</v-list-item-title>
        </v-list-item>
        <v-list-item>
          <v-list-item-action>
            <v-icon> mdi-logout </v-icon>
          </v-list-item-action>
          <v-list-item-title>Logout</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-bottom-navigation :value="value" dark shift grow>
      <v-btn to="/">
        <span>Home</span>

        <v-icon>mdi-home-outline</v-icon>
      </v-btn>

      <v-btn to="/setting">
        <span>Setting</span>

        <v-icon>mdi-cog-outline</v-icon>
      </v-btn>

      <v-btn>
        <span>Account</span>

        <v-icon>mdi-account-outline</v-icon>
      </v-btn>
    </v-bottom-navigation>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      value: 1,
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-briefcase-outline',
          title: 'Attendance',
          to: '/attendance',
        },
        {
          icon: 'mdi-wallet-plus-outline',
          title: 'Claim',
          to: '/claim',
        },
        {
          icon: 'mdi-calendar-edit',
          title: 'Schedule',
          to: '/schedule',
        },
        {
          icon: 'mdi-currency-usd',
          title: 'Salary',
          to: '/salary',
        },
        {
          icon: 'mdi-format-list-checks',
          title: 'Task',
          to: '/task',
        },
        {
          icon: 'mdi-cog-outline',
          title: 'Setting',
          to: '/setting',
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Traffic Room',
    }
  },
}
</script>
