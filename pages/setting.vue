<template>
  <v-row justify="center">
    <v-col md="6">
      <v-card>
        <v-tabs
          v-model="tabs"
          fixed-tabs
          background-color="grey darken-3"
          color="black"
          show-arrows
        >
          <v-tab> division </v-tab>
          <v-tab> schedule </v-tab>
          <v-tab> claim</v-tab>
          <v-tab> salary</v-tab>
          <v-tab> task</v-tab>
        </v-tabs>

        <v-tabs-items v-model="tabs">
          <v-tab-item> </v-tab-item>
          <v-tab-item>
            <v-row justify="center">
              <v-col cols="12">
                <v-card flat class="pa-4">
                  <v-data-table :headers="headers" :items="shift">
                    <template #top>
                      <v-toolbar>
                        <v-toolbar-title>Shift</v-toolbar-title>
                        <v-divider class="mx-4" inset vertical></v-divider>
                        <v-spacer></v-spacer>
                        <v-dialog v-model="dialog" max-width="500px">
                          <template #activator="{ on, attrs }">
                            <v-btn
                              color="primary"
                              dark
                              class="mb-2"
                              v-bind="attrs"
                              v-on="on"
                              >New Shift</v-btn
                            >
                          </template>
                          <v-card
                            v-model="valid"
                            color="grey darken-3"
                            lazy-validation
                          >
                            <v-card-title>
                              <span class="headline">
                                {{ formTitle }}
                              </span>
                            </v-card-title>
                            <v-card-text>
                              <v-row>
                                <v-col cols="12" md="6">
                                  <v-text-field
                                    v-model="editedItem.name"
                                    label="Name"
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12" md="6">
                                  <v-text-field
                                    v-model="editedItem.code"
                                    label="Code"
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12" md="6">
                                  <v-dialog
                                    ref="dialog"
                                    v-model="startPicker"
                                    :return-value.sync="editedItem.start"
                                    persistent=""
                                    width="290px"
                                  >
                                    <template #activator="{ on, attrs }">
                                      <v-text-field
                                        v-model="editedItem.start"
                                        label="Pick a time start"
                                        readonly
                                        v-bind="attrs"
                                        v-on="on"
                                      ></v-text-field>
                                    </template>
                                    <v-time-picker
                                      v-if="startPicker"
                                      v-model="defaultItem.start"
                                      format="24hr"
                                      full-width
                                    >
                                      <v-spacer></v-spacer>
                                      <v-btn text @click="startPicker = false"
                                        >Cancel</v-btn
                                      >
                                      <v-btn
                                        text
                                        @click="
                                          $refs.dialog.save(defaultItem.start)
                                        "
                                        >Ok</v-btn
                                      >
                                    </v-time-picker>
                                  </v-dialog>
                                </v-col>
                                <v-col cols="12" md="6">
                                  <v-text-field
                                    v-model="editedItem.present"
                                    type="number"
                                    min="0"
                                    max="24"
                                    :rules="presentRule"
                                    label="Present"
                                  ></v-text-field>
                                </v-col>
                              </v-row>
                            </v-card-text>
                            <v-card-actions class="pb-6">
                              <v-spacer></v-spacer>
                              <v-btn outlined @click="close">Cancel</v-btn>
                              <v-btn outlined @click="save">Save</v-btn>
                              <v-spacer></v-spacer>
                            </v-card-actions>
                          </v-card>
                        </v-dialog>
                        <v-dialog v-model="dialogDelete" max-width="500px">
                          <v-card color="grey darken-3">
                            <v-card-title class="headline"
                              >Are you sure you want to delete this
                              item?</v-card-title
                            >
                            <v-card-actions>
                              <v-spacer></v-spacer>
                              <v-btn text @click="closeDelete">Cancel</v-btn>
                              <v-btn text @click="deleteItemConfirm">OK</v-btn>
                              <v-spacer></v-spacer>
                            </v-card-actions>
                          </v-card>
                        </v-dialog>
                      </v-toolbar>
                    </template>
                    <template #[`item.code`]="{ item }">
                      <v-chip :color="getColor(item.code)" light>
                        {{ item.code }}
                      </v-chip>
                    </template>
                    <template #[`item.actions`]="{ item }">
                      <v-icon small class="mr-2" @click="editItem(item)">
                        mdi-pencil
                      </v-icon>
                      <v-icon small @click="deleteItem(item)">
                        mdi-delete
                      </v-icon>
                    </template>
                  </v-data-table>
                </v-card>
              </v-col>
            </v-row>
          </v-tab-item>
          <v-tab-item>
            <v-card flat>
              <v-card-text>claim</v-card-text>
            </v-card>
          </v-tab-item>
          <v-tab-item>
            <v-card flat>
              <v-card-text>salary</v-card-text>
            </v-card> </v-tab-item
          ><v-tab-item>
            <v-card flat>
              <v-card-text>task</v-card-text>
            </v-card>
          </v-tab-item>
        </v-tabs-items>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      valid: true,
      dialog: false,
      dialogDelete: false,
      startPicker: false,
      presentRule: [
        (v) => !!v || 'Present is required',
        (v) => (v && v > 0) || 'Must be greater than 0',
        (v) => (v && v <= 24) || 'Must be less than or equal to 24',
      ],
      tabs: null,
      editedIndex: -1,
      editedItem: {
        name: '',
        code: '',
        start: '',
        present: 0,
      },
      defaultItem: {
        name: '',
        code: '',
        start: '09:00',
        present: 0,
      },
      headers: [
        {
          text: 'Shift',
          value: 'name',
        },
        {
          text: 'Code',
          value: 'code',
          align: 'center',
          sortable: false,
        },
        {
          text: 'Start (Time)',
          value: 'start',
        },
        {
          text: 'Present (Hours)',
          value: 'present',
        },
        { text: 'Actions', value: 'actions', sortable: false },
      ],
      shift: [],
    }
  },
  computed: {
    formTitle() {
      return this.editedIndex === -1 ? 'New Shift' : 'Edit Shift'
    },
  },
  watch: {
    dialog(val) {
      val || this.close()
    },
    dialogDelete(val) {
      val || this.closeDelete()
    },
  },
  created() {
    this.initialized()
  },
  methods: {
    initialized() {
      this.shift = [
        {
          name: 'Morning',
          code: 'M',
          start: '10:00',
          present: '8',
        },
        {
          name: 'Middle',
          code: 'Md',
          start: '12:00',
          present: '8',
        },
        {
          name: 'Afternoon',
          code: 'Af',
          start: '14:00',
          present: '8',
        },
      ]
    },
    editItem(item) {
      this.editedIndex = this.shift.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.dialog = true
    },
    deleteItem(item) {
      this.editedIndex = this.shift.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.dialogDelete = true
    },
    deleteItemConfirm() {
      this.shift.splice(this.editedIndex, 1)
      this.closeDelete()
    },
    close() {
      this.dialog = false
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem)
        this.editedIndex = -1
      })
    },
    closeDelete() {
      this.dialogDelete = false
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem)
        this.editedIndex = -1
      })
    },
    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.shift[this.editedIndex], this.editedItem)
      } else {
        this.shift.push(this.editedItem)
      }
      this.close()
    },
    getColor(code) {
      if (code === 'M') return 'green'
      else if (code === 'Md') return 'yellow'
      else return 'red'
    },
  },
}
</script>
