<template>
  <div>
    <v-card class="pb-12">
      <v-card-actions class="d-flex justify-end pa-2">
        <v-btn icon @click="closeDialog()">
          <v-icon size="20px">mdi-close</v-icon>
        </v-btn>
      </v-card-actions>
      <v-card-title>
        <DialogSection icon="mdi-square" :color="event.color || 'blue'">
          {{ event.name }}
        </DialogSection>
      </v-card-title>
      <v-card-text>
        <DialogSection icon="mdi-clock-time-three-outline">
          {{ event.start.toLocaleString() }} ~ {{ event.end.toLocaleString() }}
        </DialogSection>
      </v-card-text>
      <v-card-text>
        <DialogSection icon="mdi-card-text-outline">
          {{ event.description || 'no description' }}
        </DialogSection>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';
import DialogSection from './DialogSection.vue';

export default {
  name: 'EventDetailDialog',
  computed: {
    ...mapGetters('events', ['event']),
  },
  components: {
    DialogSection,
  },
  methods: {
    ...mapActions('events', ['setEventActions']),
    closeDialog() {
      this.setEventActions(null);
    },
  },
};
</script>
