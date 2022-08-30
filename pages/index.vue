<template>
  <v-row justify="center" align="center">
    <v-col>
      <!--
      <v-card class="logo py-4 d-flex justify-center">
        <NuxtLogo />
        <VuetifyLogo />
      </v-card>
      -->
      <v-card>
        <p class="title text-center">
          <v-alert
            dense
            border="bottom"
          >
          Promoções
          </v-alert>
        </p>
        <v-list
          elevation="3"
        >
          <v-subheader>General</v-subheader>

          <v-list-item>
            <v-list-item-avatar tile size="80">
                <v-img
                  alt="avatar"
                  src="https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg"
                ></v-img>
              </v-list-item-avatar>
            <v-list-item-content>
              <v-list-item-title>Profile photo</v-list-item-title>
              <v-list-item-subtitle>Change your Google+ profile photo</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
          <v-divider></v-divider>
          <v-list-item>
            <v-list-item-avatar tile size="80">
                <v-img
                  tile
                  alt="avatar"
                  src="https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg"
                ></v-img>
              </v-list-item-avatar>
            <v-list-item-content>
              <v-list-item-title>Show your status</v-list-item-title>
              <v-list-item-subtitle>Your status is visible to everyone</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list>

        <v-divider></v-divider>
      </v-card>
      <v-card>
        <p class="title text-center">
          <v-alert
            dense
            border="bottom"
          >
          Combos
          </v-alert></p>
        <v-list
          elevation="3"
        >
          <v-subheader>General</v-subheader>

          <v-list-item>
            <v-list-item-avatar tile size="80">
                <v-img
                  alt="avatar"
                  src="https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg"
                ></v-img>
              </v-list-item-avatar>
            <v-list-item-content>
              <v-list-item-title>Profile photo</v-list-item-title>
              <v-list-item-subtitle>Change your Google+ profile photo</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
          <v-divider></v-divider>
          <v-list-item>
            <v-list-item-avatar tile size="80">
                <v-img
                  tile
                  alt="avatar"
                  src="https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg"
                ></v-img>
              </v-list-item-avatar>
            <v-list-item-content>
              <v-list-item-title>Show your status</v-list-item-title>
              <v-list-item-subtitle>Your status is visible to everyone</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list>

        <v-divider></v-divider>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage'
}
</script>
