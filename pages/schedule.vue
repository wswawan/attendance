<template>
  <div>
    <v-row justify="center">
      <v-col md="3">
        <v-card>
          <v-card-text>
            <v-dialog
              ref="dialog"
              v-model="modal"
              :return-value.sync="date"
              persistent
              width="290px"
            >
              <template #activator="{ on, attrs }">
                <v-text-field
                  v-model="date"
                  label="Date"
                  prepend-icon="mdi-calendar"
                  readonly
                  v-bind="attrs"
                  v-on="on"
                ></v-text-field>
              </template>
              <v-date-picker v-model="date" scrollable>
                <v-spacer></v-spacer>
                <v-btn text color="primary" @click="modal = false">
                  Cancel
                </v-btn>
                <v-btn text color="primary" @click="$refs.dialog.save(date)">
                  OK
                </v-btn>
              </v-date-picker>
            </v-dialog>
          </v-card-text>
          <v-card-text>
            <v-select
              v-model="e7"
              :items="users"
              label="Select"
              prepend-icon="mdi-account-outline"
              multiple
              chips
              hint="Choose users"
              persistent-hint
            ></v-select>
          </v-card-text>
          <v-card-text>
            <v-select
              v-model="timesheet"
              :items="timesheets"
              menu-props="auto"
              label="Select Schedule"
              hide-details
              prepend-icon="mdi-calendar-text-outline"
              single-line
            ></v-select>
          </v-card-text>
          <v-divider></v-divider>
          <v-card-actions>
            <v-btn block>Submit</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>
<script>
export default {
  data: () => ({
    date: new Date().toISOString().substr(0, 10),
    menu: false,
    modal: false,
    e7: [],
    users: ['Fajar', 'Fahri', 'Adi', 'Dio', 'Bagus'],
    timesheet: [],
    timesheets: ['Morning', 'Afternoon', 'Middle'],
  }),
}
</script>
