<template>
  <v-card class="pb-12">
    <v-card-actions class="d-flex justify-end pa-2">
      <v-btn icon @click="closeDialog">
        <v-icon size="20px">mdi-close</v-icon>
      </v-btn>
    </v-card-actions>
    <v-card-text>
      <DialogSection icon="mdi-square" :color="event.color || 'blue'">
        <v-text-field v-model="name" label="タイトル"></v-text-field>
      </DialogSection>
      <DialogSection icon="mdi-clock-outline">
        <DateForm v-model="startDate" />
        <DateForm v-model="endDate" />
      </DialogSection>
    </v-card-text>
    <v-card-actions class="d-flex justify-end">
      <v-btn @click="submit">保存</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';
import DialogSection from './DialogSection.vue';
import DateForm from './DateForm.vue';
import { format } from 'date-fns';

export default {
  name: 'EventFormDialog',
  components: {
    DialogSection,
    DateForm,
  },
  data: () => ({
    name: '',
    startDate: null,
    endDate: null,
  }),
  computed: {
    ...mapGetters('events', ['event']),
  },
  created() {
    // dataで初期化したstartDate変数に、カレンダーでクリックした時の日付を文字列に変換して代入
    this.startDate = format(this.event.start, 'yyyy/MM/dd');
    this.endDate = format(this.event.end, 'yyyy/MM/dd');
  },
  methods: {
    ...mapActions('events', ['setEventActions', 'setEditMode', 'createEvent']),
    closeDialog() {
      this.setEventActions(null);
      this.setEditMode(false);
    },
    submit() {
      const params = {
        name: this.name,
        start: this.startDate,
        end: this.endDate,
      };
      this.createEvent(params);
      this.closeDialog();
    },
  },
};
</script>
