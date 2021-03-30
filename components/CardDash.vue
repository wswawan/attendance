<template>
  <v-row class="text-center" justify="center" dense>
    <v-col v-for="(item, i) in items" :key="i" md="1" cols="4">
      <v-card>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-avatar>
              <v-icon size="48" :color="item.colorIcon">{{ item.icon }}</v-icon>
            </v-list-item-avatar>
            <v-list-item-subtitle>{{ item.title }}</v-list-item-subtitle>
            <v-list-item-subtitle class="caption">
              <span v-if="item.title === 'Over Time' || item.title === 'Late'">
                {{ item.countMinute }} Minutes
              </span>
              <span v-else>
                {{ item.countDays }} Day{{ item.countDays > 1 ? 's' : '' }}
              </span>
            </v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          icon: 'mdi-fingerprint',
          colorIcon: 'green lighten-3',
          title: 'Present',
          countDays: '10',
          countMinute: '320',
        },
        {
          icon: 'mdi-fingerprint-off',
          colorIcon: 'red lighten-3',
          title: 'OFF',
          countDays: '1',
          countMinute: '',
        },
        {
          icon: 'mdi-clock-alert-outline',
          colorIcon: 'yellow lighten-3',
          title: 'Late',
          countDays: '14',
          countMinute: '320',
        },
        {
          icon: 'mdi-timelapse',
          colorIcon: '',
          title: 'Over Time',
          countDays: '2',
          countMinute: '120',
        },
        {
          icon: 'mdi-wallet-travel',
          colorIcon: '',
          title: 'Paid Leave',
          countDays: '2',
          countMinute: '320',
        },
        {
          icon: 'mdi-email-alert',
          colorIcon: 'red',
          title: 'Permit',
          countDays: '6',
          countMinute: '320',
        },
      ],
    }
  },
}
</script>
