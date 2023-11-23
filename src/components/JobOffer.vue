<template>
  <v-container class="mt-2 ml-1 mr-1">
    <v-responsive class="align-center text-center fill-height">
      <v-card
        width="400"
        :title="this.title"
        style="
          border-radius: 10px;
          border-color: rgb(220, 11, 11);
          border: solid 0.05em;
          outline: 2em;
        "
      >
        <v-container class="description">
          <v-dialog transition="dialog-bottom-transition" width="auto">
            <template v-slot:activator="{ props }">
              <v-btn
                append-icon="mdi-information-outline"
                color="secondary"
                v-bind="props"
                >Stellenbeschreibung</v-btn
              >
            </template>
            <template v-slot:default="{ isActive }">
              <v-card>
                <v-toolbar
                  color="rgb(30, 110, 150)"
                  title="Stellenbeschreibung"
                ></v-toolbar>
                <v-card-text>
                  <div class="pa-12">{{ description }}</div>
                </v-card-text>
                <v-card-actions class="justify-end">
                  <v-btn
                    color="red"
                    class="mr-auto"
                    variant="text"
                    @click="isActive.value = false"
                    >Schliessen</v-btn
                  >
                </v-card-actions>
              </v-card>
            </template>
          </v-dialog>
        </v-container>
        <div class="vertical-align">
          <v-row class="">
            <v-col class="vertical-align">
              <div class="mdi mdi-cash-100 mr-1" style="color: green"></div>
              <div class="mr-1">Stundenlohn:</div>
            </v-col>
            <v-col>{{ salary }}</v-col>
          </v-row>
        </div>
        <v-divider></v-divider>

        <div>
          <v-row>
            <v-col class="vertical-align">
              <div
                class="mdi mdi-clock-outline mr-1"
                style="color: orange"
              ></div>
              <div class="mr-1">Arbeitszeiten:</div>
            </v-col>

            <v-col>{{ workTime }}</v-col>
          </v-row>
        </div>
        <v-divider></v-divider>

        <div>
          <v-row>
            <v-col class="vertical-align">
              <div class="mdi mdi-calendar mr-1" style="color: blue"></div>
              <div class="mr-1">Datum:</div>
            </v-col>

            <v-col>{{ date }}</v-col>
          </v-row>
        </div>
        <v-divider></v-divider>

        <div v-if="prerequisites != null && prerequisites != undefined">
          <v-row>
            <v-col class="vertical-align">
              <div
                class="mdi mdi-account-star mr-1"
                style="color: purple"
              ></div>
              <div class="mr-1">Voraussetzung:</div>
            </v-col>

            <v-col>{{ prerequisites }}</v-col>
          </v-row>
        </div>

        <v-divider></v-divider>

        <v-dialog width="500">
          <template v-slot:activator="{ props }">
            <v-btn
              class="mt-2 mb-2"
              v-bind="props"
              v-if="!hasApplied"
              text="Bewerben"
              color="primary"
            >
            </v-btn>
            <v-btn
              class="mt-2"
              append-icon="mdi-check"
              v-if="hasApplied"
              text="Sie haben sich beworben"
              color="green"
              disabled
              slim
            >
            </v-btn>
            <v-container class="center" v-if="hasApplied">
              <div>Status: Warte auf Rückmeldung</div>
            </v-container>
          </template>

          <template v-slot:default="{ isActive }">
            <v-card title="Bestätigung">
              <v-card-text>
                Hiermit bestätigen Sie, dass Sie sich tatsächlich für die
                ausgeschriebene Stelle "{{ title }}" bewerben möchten.
              </v-card-text>

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-row>
                  <v-col>
                    <v-btn
                      color="red"
                      text="Abbrechen"
                      @click="isActive.value = false"
                    ></v-btn>
                  </v-col>
                  <v-col
                    ><v-btn
                      color="green"
                      text="Akzeptieren"
                      @click="
                        (isActive.value = false),
                          (hasApplied = true),
                          sendAcceptanceToBackEnd
                      "
                    ></v-btn
                  ></v-col>
                </v-row>
              </v-card-actions>
            </v-card>
          </template>
        </v-dialog>
      </v-card>
    </v-responsive>
  </v-container>
</template>

<script>
//
export default {
  props: {
    title: String,
    description: String,
    salary: String,
    workTime: String,
    date: String,
    prerequisites: String,
  },
  data() {
    return {
      doApply: false,
      hasApplied: false,
    };
  },
  methods: {
    toggleApply() {
      this.doApply = true;
    },
    sendAcceptanceToBackEnd() {
      //Die Bewerbung des Users wird hier an das Backend weitergeleitet
    },
  },
};
</script>

<style>
.vertical-align {
  display: flex;
  align-items: center;
}

.vertical-align-2 {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}

.center {
  margin: auto, auto, auto, auto;
}
</style>
