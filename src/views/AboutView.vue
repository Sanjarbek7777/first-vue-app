<template>
  <div class="about">
    <v-card max-width="400px" class="mx-auto mt-5">
      <v-toolbar color="success">
        <v-toolbar-title> Input card </v-toolbar-title>
      </v-toolbar>
      <v-divider></v-divider>
      <v-card-text>
        <v-text-field label="Main input" outlined dense></v-text-field>
        <v-text-field label="Another input" outlined dense></v-text-field>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="success" dark>Submit</v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>
