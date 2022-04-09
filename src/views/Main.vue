<template>
  <div>
    <v-container>
      <v-row>
        <v-col>
          {{ routerParams }}
          <v-card class="mx-auto" max-width="344">
            <v-card-title> New Container Terminal </v-card-title>

            <v-card-actions>
              <v-btn
                color="orange lighten-2"
                text
                @click.native="$router.push('/new-container')"
              >
                Go</v-btn
              >

              <v-spacer></v-spacer>
            </v-card-actions>

            <v-expand-transition>
              <div v-show="show">
                <v-divider></v-divider>

                <v-card-text>
                  I'm a thing. But, like most politicians, he promised more than
                  he could deliver. You won't have time for sleeping, soldier,
                  not with all the bed making you'll be doing. Then we'll go
                  with that data file! Hey, you add a one and two zeros to that
                  or we walk! You're going to do his laundry? I've got to find a
                  way to escape.
                </v-card-text>
              </div>
            </v-expand-transition>
          </v-card>
        </v-col>
        <v-col>
          <v-card class="mx-auto" max-width="344">
            <v-card-title>Existing Container Terminal</v-card-title>

            <v-card-actions>
              <v-btn
                color="orange lighten-2"
                text
                @click.native="$router.push('/existing-container')"
              >
                Go</v-btn
              >

              <v-spacer></v-spacer>
            </v-card-actions>

            <v-expand-transition>
              <div v-show="show">
                <v-divider></v-divider>

                <v-card-text>
                  I'm a thing. But, like most politicians, he promised more than
                  he could deliver. You won't have time for sleeping, soldier,
                  not with all the bed making you'll be doing. Then we'll go
                  with that data file! Hey, you add a one and two zeros to that
                  or we walk! You're going to do his laundry? I've got to find a
                  way to escape.
                </v-card-text>
              </div>
            </v-expand-transition>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {

};
</script>

<style>
</style>