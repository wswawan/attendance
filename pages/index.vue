<template>
  <div>
    <div v-for="attendance in attendances" :key="attendance.id">
      <div class="ma-2 text-center">
        <h3>{{ attendance.name }}</h3>
      </div>
      <v-divider class="ma-3"></v-divider>
      <v-row justify="center" dense>
        <v-col
          v-for="(item, i) in attendance.items"
          :key="i"
          md="1"
          cols="4"
          class="text-center"
        >
          <v-btn fab :to="item.to">
            <v-icon :color="item.color">{{ item.icon }}</v-icon>
          </v-btn>
          <v-list-item-subtitle class="mt-2 text-wrap text-caption">{{
            item.title
          }}</v-list-item-subtitle>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      attendances: [
        {
          id: 1,
          name: 'Attendance',
          items: [
            {
              icon: 'mdi-fingerprint',
              color: 'green lighten-3',
              title: 'Check In',
              to: '/checkIn',
            },
            {
              icon: 'mdi-coffee',
              color: 'green lighten-3',
              title: 'Break In',
            },
            {
              icon: 'mdi-timelapse',
              color: 'green lighten-3',
              title: 'Overtime In',
            },
            {
              icon: 'mdi-fingerprint-off',
              color: 'red lighten-3',
              title: 'Check Out',
            },
            {
              icon: 'mdi-coffee-off',
              color: 'red lighten-3',
              title: 'Break Out',
            },
            {
              icon: 'mdi-av-timer',
              color: 'red lighten-3',
              title: 'Overtime Out',
            },
          ],
        },
        {
          id: 2,
          name: 'Others',
          items: [
            {
              icon: 'mdi-calendar-edit',
              title: 'Schedule',
              to: '/schedule',
            },
            {
              icon: 'mdi-wallet-plus-outline',
              title: 'Claim',
              to: '/claim',
            },
            {
              icon: 'mdi-format-list-checks',
              title: 'Task',
              to: '/task',
            },
          ],
        },
      ],
    }
  },
}
</script>
