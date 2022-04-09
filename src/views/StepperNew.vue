<template>
  <div>
    <v-stepper v-model="routerParams">
      <v-stepper-header>
        <v-stepper-step :complete="routerParams > 1" step="1"> </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step :complete="routerParams > 2" step="2"> </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step :complete="routerParams > 3" step="3"></v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step :complete="routerParams > 4" step="4"> </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step :complete="routerParams > 5" step="5"> </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step :complete="routerParams > 6" step="6"></v-stepper-step>
      </v-stepper-header>

      <v-stepper-items>
        <v-stepper-content step="1">
          <v-card elevation="0" class="mb-12">
            <v-container>
              <v-row>
                <v-col>
                  <h2 class="text-center">General Assumptions</h2>
                  <v-text-field
                    label="Minimum terminal capacity"
                    outlined
                    suffix="TEU/Year"
                  ></v-text-field>
                  <v-text-field
                    label="TEU factor"
                    @click:append="teuShow = !teuShow"
                    outlined
                    :append-icon="teuShow ? 'mdi-eye' : 'mdi-eye-off'"
                    :type="teuShow ? 'text' : 'password'"
                  ></v-text-field>
                  <v-text-field
                    label="Shore Crane Productivity (BCH)"
                    outlined
                    suffix="Moves/Hour"
                  ></v-text-field>
                </v-col>
                <v-col>
                  <h2 class="text-center">Berth Assumptions</h2>
                  <v-text-field
                    label="Quay Length"
                    outlined
                    suffix="meters"
                  ></v-text-field>
                  <v-text-field
                    label="LOA Vessel"
                    outlined
                    suffix="meters"
                  ></v-text-field>
                  <v-text-field
                    label="Vessel Movements (TEU Dish & Load)"
                    outlined
                    suffix="TEUS"
                  ></v-text-field>
                  <v-text-field
                    label="Crane Ration per Vessel"
                    outlined
                    suffix="unit/ship"
                  ></v-text-field>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <h2 class="text-center">Get In & Out Assumptions</h2>
                  <v-text-field
                    label="Number of Get In"
                    outlined
                    suffix="Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Avg Process Time at Gate In"
                    outlined
                    suffix="second/truck"
                  ></v-text-field>
                  <v-text-field
                    label="Gate Peak Factor"
                    outlined
                    suffix="days"
                  ></v-text-field>
                  <v-text-field
                    label="Number of Gate Out"
                    outlined
                    suffix="unit"
                  ></v-text-field>
                  <v-text-field
                    label="Avg Process Time at Gate Out"
                    outlined
                    suffix="second/truck"
                  ></v-text-field>
                  <v-text-field
                    label="Transhipment Ration"
                    outlined
                    suffix="%"
                  ></v-text-field>
                </v-col>
                <v-col>
                  <h2 class="text-center">Internal Truck Assumptions</h2>
                  <v-text-field
                    label="Average Truck Cycle Time"
                    outlined
                    suffix="second/truck"
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card>

          <v-btn color="primary" @click="routerParams += 1"> Submit </v-btn>

          <v-btn text @click="routerParams -= 1"> Back </v-btn>
        </v-stepper-content>

        <v-stepper-content step="2">
          <v-card elevation="0" class="mb-12">
            <chart :chartId="'new'" :chartData="chartData" />
            <v-text-field
              label="Terminal Capacity"
              value="501.072"
              outlined
              suffix="TEUS"
              readonly
            >
              <template v-slot:append-outer>
                <v-btn color="secondary">See Detail</v-btn>
              </template>
            </v-text-field>
            <v-text-field
              label="Minimum Terminal Capacity Required"
              value="500.000"
              readonly
              outlined
              suffix="TEUS"
            >
              <template v-slot:append-outer>
                <v-btn color="secondary">See Detail</v-btn>
              </template>
            </v-text-field>
          </v-card>

          <v-btn color="primary" @click="routerParams += 1"> Next </v-btn>

          <v-btn text @click="routerParams -= 1"> Cancel </v-btn>
        </v-stepper-content>

        <v-stepper-content step="3">
          <v-card class="mb-12" elevation="0">
            <v-container>
              <v-row>
                <v-col>
                  <h3>Target Container Terminal Capacity (TEUS)</h3>
                  <h4 class="text-center font-italic">
                    To build your new container terminal with capacty of
                  </h4>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <v-text-field
                    value="501.072"
                    readonly
                    outlined
                    suffix="TEU/Year"
                  ></v-text-field>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <h3>You may need to have</h3>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <ul>
                    <li>400 meter quay length</li>
                    <li>15.000 TEUS effective yard capacity</li>
                    <li>2 unit of gate in</li>
                    <li>1 unit of gate out</li>
                    <li>Add 6 Internal Truck</li>
                  </ul>
                </v-col>
                <v-col>
                  <ul>
                    <li>4 shore cranes</li>
                    <li>2 Reach stackers</li>
                    <li>7 RTG</li>
                  </ul>
                </v-col>
              </v-row>
              <p>
                Please remember to do the financial and commercial feasibility
                study before take your decision
              </p>
            </v-container>
          </v-card>

          <v-btn color="primary" @click="routerParams += 1"> Next </v-btn>

          <v-btn text @click="routerParams -= 1"> Cancel </v-btn>
        </v-stepper-content>

        <v-stepper-content step="4">
          <v-card class="mb-12" elevation="0">
            <v-container>
              <h2>Man Power Assumptions</h2>
              <v-row>
                <v-col>
                  <v-text-field
                    label="Additional Traffic Man"
                    outlined
                    suffix="person/group"
                  ></v-text-field>
                  <v-text-field
                    label="Additional Planner"
                    outlined
                    suffix="person/group"
                  ></v-text-field>
                  <v-text-field
                    label="Total Manpower Group"
                    outlined
                    suffix="group"
                  ></v-text-field>
                  <v-text-field
                    label="Permanent Employee Salary"
                    outlined
                    suffix="Rp/group"
                  ></v-text-field>
                  <v-text-field
                    label="Contract Employee Salary"
                    outlined
                    suffix="Rp/group"
                  ></v-text-field>
                </v-col>
                <v-col>
                  <div class="d-flex justify-space-between align-center">
                    <h4>Yard Operator Assistant (OA)</h4>
                    <v-radio-group row>
                      <v-radio label="No" value="radio-1"></v-radio>
                      <v-radio label="Yes" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between align-center">
                    <h4>SC Operator</h4>
                    <v-radio-group row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between align-center">
                    <h4>Solo</h4>
                    <v-radio-group row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between align-center">
                    <h4>Whisky</h4>
                    <v-radio-group row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between align-center">
                    <h4>YC Operator</h4>
                    <v-radio-group row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between align-center">
                    <h4>Yard OA</h4>
                    <v-radio-group row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between align-center">
                    <h4>ITT Operator</h4>
                    <v-radio-group row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between align-center">
                    <h4>Gate Officer</h4>
                    <v-radio-group row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between align-center">
                    <h4>Gate Inspector</h4>
                    <v-radio-group row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between align-center">
                    <h4>Traffic Man</h4>
                    <v-radio-group row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between align-center">
                    <h4>Planner</h4>
                    <v-radio-group row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                </v-col>
              </v-row>
            </v-container>
          </v-card>

          <v-btn color="primary" @click="routerParams += 1"> Next </v-btn>

          <v-btn text @click="routerParams -= 1"> Cancel </v-btn>
        </v-stepper-content>

        <v-stepper-content step="5">
          <v-card elevation="0" class="mb-12">
            <v-container>
              <h2>Equipment Assumptions</h2>
              <v-row>
                <v-col>
                  <v-text-field
                    label="QCC"
                    outlined
                    suffix="Liter/Hour"
                  ></v-text-field>
                  <v-text-field
                    label="HMC"
                    outlined
                    suffix="Liter/Hour"
                  ></v-text-field>
                  <v-text-field
                    label="Reach Stacker"
                    outlined
                    suffix="Liter/Hour"
                  ></v-text-field>
                  <v-text-field
                    label="Side Loader"
                    outlined
                    suffix="Liter/Hour"
                  ></v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                    label="RTGC"
                    outlined
                    suffix="Liter/Hour"
                  ></v-text-field>
                  <v-text-field
                    label="RMGC"
                    outlined
                    suffix="Liter/Hour"
                  ></v-text-field>
                  <v-text-field
                    label="Internal Truck"
                    outlined
                    suffix="Liter/Hour"
                  ></v-text-field>
                  <v-text-field
                    label="Fuel Price"
                    outlined
                    suffix="Rupiah/Liter"
                  ></v-text-field>
                </v-col>
              </v-row>

              <v-row>
                <v-col>
                  <h2>Yard Assumptions</h2>
                  <v-text-field
                    label="Tier Max in Storage Yard"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Stacking Area/Yard Area"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Berth Wide"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Pavement Type"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Investment Cost/m2"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                </v-col>
                <v-col>
                  <h2>Berth Assumptions</h2>
                  <v-row>
                    <v-col>
                      <v-text-field
                        label="Structure Type"
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col>
                      <v-text-field
                        label="Inv Cost / M2"
                        outlined
                        suffix="meters"
                      ></v-text-field>
                    </v-col>
                  </v-row>

                  <h2>Gate Assumptions</h2>
                  <v-row>
                    <v-col>
                      <v-text-field
                        label="Inv Cost / m2 (Gate In)"
                        outlined
                        suffix="Rp/m2"
                      ></v-text-field>
                    </v-col>
                    <v-col>
                      <v-text-field
                        label="Inv Cost / M2 (Gate Out)"
                        outlined
                        suffix="Rp/m2"
                      ></v-text-field>
                    </v-col>
                  </v-row>

                  <h2>Weighing Scale</h2>
                  <v-row>
                    <v-col>
                      <v-text-field
                        label="Inv Cost / m2 (Gate In)"
                        outlined
                        suffix="Rp/m2"
                      ></v-text-field>
                    </v-col>
                  </v-row>
                </v-col>
              </v-row>

              <h2>IT Infrastructure Assumptions</h2>
              <v-row>
                <v-col>
                  <v-text-field
                    label="Gate In"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Gate Out"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Yard"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Berth"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                    label="Equipment (VMT)"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Equipment (Pager)"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Equipment (Handheld)"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Constrol Tower"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                </v-col>
              </v-row>

              <v-row>
                <v-col>
                  <h2>Investment Cost Impact Estimation Due To Improvements</h2>

                  <h3>Equipment</h3>
                  <v-text-field
                    label="1 HMC, 2 RTG, 6 ITT"
                    value="XXX.XXX.XXX"
                    outlined
                    suffix="Rupiah"
                  ></v-text-field>

                  <h3>Facility</h3>
                  <v-text-field
                    label="Yard"
                    value="XXX.XXX.XXX"
                    outlined
                    suffix="Rupiah"
                  ></v-text-field>
                  <v-text-field
                    label="Berth"
                    value="XXX.XXX.XXX"
                    outlined
                    suffix="Rupiah"
                  ></v-text-field>
                  <v-text-field
                    label="Gate"
                    value="XXX.XXX.XXX"
                    outlined
                    suffix="Rupiah"
                  ></v-text-field>

                  <v-divider></v-divider>

                  <v-text-field
                    label="IT Infrastructure"
                    value="XXX.XXX.XXX"
                    outlined
                    suffix="Rupiah"
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card>

          <v-btn color="primary" @click="routerParams += 1"> Next </v-btn>
          <v-btn text @click="routerParams -= 1"> Cancel </v-btn>
        </v-stepper-content>

        <v-stepper-content step="6">
          <v-card class="mb-12" elevation="0">
            <h1 class="text-center">Check the diagnosis Summary</h1>

            <v-container>
              <v-row>
                <v-col>
                  <v-text-field
                    readonly
                    label="Current Terminal Capacity"
                    outlined
                    value="375.804"
                    suffix="TEUS"
                  ></v-text-field>

                  <v-text-field
                    readonly
                    label="Target Terminal Capacity"
                    outlined
                    value="501.072"
                    suffix="TEUS"
                  ></v-text-field>

                  <v-divider></v-divider>

                  <h3>Recommendation for Improvement</h3>
                  <ul>
                    <li>Increase your quay lenght by 100 meter</li>
                    <li>Increase your effective yard capacty by 5.000</li>
                    <li>Add 2 RTG</li>
                    <li>Add 6 Internal Truck</li>
                  </ul>

                  <v-divider></v-divider>

                  <h4 class="mt-5 mb-3">Manpower Cost Gap Estimation / Year</h4>
                  <v-text-field
                    readonly
                    label="Cost GAP"
                    outlined
                    value="4.713.601.564"
                    suffix="Rupiah"
                  >
                  </v-text-field>

                  <h4 class="mb-3">Fuel Cost Gap Estimation / Year</h4>
                  <v-text-field
                    readonly
                    label="Cost GAP"
                    outlined
                    value="4.713.601.564"
                    suffix="Rupiah"
                  >
                  </v-text-field>
                </v-col>
                <v-col>
                  <h3>Investment Cost Impact Estimation</h3>

                  <h4 class="mt-5 mb-3">Equipment</h4>
                  <v-text-field
                    readonly
                    label="1 HMC, 2 RTG, 6 ITT"
                    outlined
                    value="72.900.000.000"
                    suffix="Rupiah"
                  >
                    <template v-slot:append-outer>
                      <v-btn color="secondary">See Detail</v-btn>
                    </template>
                  </v-text-field>

                  <h4 class="mt-5 mb-3">Facility</h4>
                  <v-text-field
                    readonly
                    label="Yard"
                    outlined
                    value="375.000.000.000"
                    suffix="Rupiah"
                  >
                    <template v-slot:append-outer>
                      <v-btn color="secondary">See Detail</v-btn>
                    </template>
                  </v-text-field>
                  <v-text-field
                    readonly
                    label="Berth"
                    outlined
                    value="200.000.000.000"
                    suffix="Rupiah"
                  >
                    <template v-slot:append-outer>
                      <v-btn color="secondary">See Detail</v-btn>
                    </template>
                  </v-text-field>
                  <v-text-field
                    readonly
                    label="Gate"
                    outlined
                    value="0"
                    suffix="Rupiah"
                  >
                    <template v-slot:append-outer>
                      <v-btn color="secondary">See Detail</v-btn>
                    </template>
                  </v-text-field>
                  <v-text-field
                    readonly
                    label="IT Infrastructure"
                    outlined
                    value="1.000.000.000"
                    suffix="Rupiah"
                  >
                    <template v-slot:append-outer>
                      <v-btn color="secondary">See Detail</v-btn>
                    </template>
                  </v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card>

          <v-btn color="primary" @click="routerParams += 1"> Complete</v-btn>
          <v-btn text @click="routerParams -= 1">Cancel</v-btn>
        </v-stepper-content>
      </v-stepper-items>
    </v-stepper>
  </div>
</template>

<script>
import Chart from "@/components/Chart";

export default {
  components: { Chart },
  data() {
    return {
      e1: this.$route.path,
      peakFactor: false,
      teuShow: true,
      shareCraneWorkHourShow: true,
      yardCraneWorkHourShow: true,
      chartData: {
        labels: [
          "Berth",
          "Yard",
          "Shore Crane",
          "Yard Crane",
          "Get In",
          "Get Out",
        ],
        datasets: [
          {
            label: "Existing Container Terminal Capacity (TEUS)",
            data: [416245, 393077, 375804, 412070, 573382, 573382],
            backgroundColor: [
              "rgba(255, 99, 132, 0.2)",
              "rgba(255, 159, 64, 0.2)",
              "rgba(255, 205, 86, 0.2)",
              "rgba(75, 192, 192, 0.2)",
              "rgba(54, 162, 235, 0.2)",
              "rgba(153, 102, 255, 0.2)",
              "rgba(201, 203, 207, 0.2)",
            ],
          },
        ],
      },
      chartOptions: {
        responsive: true,
      },
    };
  },
  methods: {
    completed() {
      console.log("yes!");
    },
  },
  computed: {
    routerParams: {
      get: function () {
        return parseInt(this.$route.query.id);
      },
      set: function (args) {
        return this.$router.push({
          path: this.$route.path,
          query: { id: args },
        });
      },
    },
  },
};
</script>

<style>
h2 {
  padding: 5px;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
  margin-bottom: 10px;
  color: white;
  background-color: #30ccfd;
}

h3 {
  padding: 5px;
  border-bottom-right-radius: 10px;
  margin-bottom: 10px;
  color: #30ccfd;
  background-color: #0e2d61;
}

h1 {
  padding: 5px;
  border-bottom-right-radius: 10px;
  border-bottom-left-radius: 10px;
  margin-bottom: 10px;
  color: #30ccfd;
  background-color: #0e2d61;
}
</style>