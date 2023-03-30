<template>
  <v-dialog
    v-model="dialogVisible"
    transition="dialog-top-transition"
    max-width="600"
  >
    <!-- <template v-slot:activator="{ on, attrs }">
        <v-btn color="primary" v-bind="attrs" v-on="on">Open Dialog</v-btn>
      </template> -->
    <v-card>
      <v-toolbar color="primary" dark>
        <v-toolbar-title>{{ operation }}</v-toolbar-title>
      </v-toolbar>
      <v-card-text>
        <div class="text-h2 pa-12">{{ description }}</div>
      </v-card-text>
      <v-card-actions class="justify-end">
        <v-btn text @click="closeDialog">Close</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  props: ['operation', 'description'],
  data() {
    return {
      dialogVisible: false,

    };
  },
  methods: {
    closeDialog() {
      this.dialogVisible = false;
    },
  },
};
</script>
