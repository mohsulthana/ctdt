<template>
  <div>
    <v-stepper v-model="routerParams">
      <v-stepper-header>
        <v-stepper-step :complete="routerParams > 1" step="1"> </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step :complete="e1 > 2" step="2"> </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step :complete="e1 > 3" step="3"></v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step :complete="e1 > 4" step="4"> </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step :complete="e1 > 5" step="5"> </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step :complete="e1 > 6" step="6"></v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step :complete="e1 > 7" step="7"> </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step :complete="routerParams == 8" step="8"> </v-stepper-step>
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
                  <h2 class="text-center">Yard Assumptions</h2>
                  <v-text-field
                    label="Effective Yard Capacity"
                    outlined
                    suffix="TEU"
                  ></v-text-field>
                  <v-text-field
                    label="Maximum Utilization"
                    outlined
                    suffix="%"
                  ></v-text-field>
                  <v-text-field
                    label="Dwell Time"
                    outlined
                    suffix="days"
                  ></v-text-field>
                </v-col>
                <v-col>
                  <h2 class="text-center">Shore & Yard Crane Assumptions</h2>
                  <v-text-field
                    label="Share Crane Workhour/Year"
                    outlined
                    suffix="%"
                    @click:append="
                      shareCraneWorkHourShow = !shareCraneWorkHourShow
                    "
                    :append-icon="
                      shareCraneWorkHourShow ? 'mdi-eye' : 'mdi-eye-off'
                    "
                    :type="shareCraneWorkHourShow ? 'text' : 'password'"
                  ></v-text-field>
                  <v-text-field
                    label="Yard Crane Workhour/Year"
                    outlined
                    suffix="%"
                    @click:append="
                      yardCraneWorkHourShow = !yardCraneWorkHourShow
                    "
                    :append-icon="
                      yardCraneWorkHourShow ? 'mdi-eye' : 'mdi-eye-off'
                    "
                    :type="yardCraneWorkHourShow ? 'text' : 'password'"
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card>
          <v-btn color="primary" @click="routerParams += 1"> Next </v-btn>
          <v-btn text @click="routerParams = 1"> Cancel </v-btn>
        </v-stepper-content>

        <v-stepper-content step="2">
          <v-card elevation="0" class="mb-12">
            <chart :chartId="'current'" :chartData="currentChartData" />
          </v-card>

          <v-btn color="primary" @click="routerParams += 1"> Next </v-btn>
          <v-btn text @click="routerParams = 1"> Back </v-btn>
        </v-stepper-content>

        <v-stepper-content step="3">
          <v-card class="mb-12" elevation="0">
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
                  <h2 class="text-center">Yard Assumptions</h2>
                  <v-text-field
                    label="Effective Yard Capacity"
                    outlined
                    suffix="TEU"
                  ></v-text-field>
                  <v-text-field
                    label="Maximum Utilization"
                    outlined
                    suffix="%"
                  ></v-text-field>
                  <v-text-field
                    label="Dwell Time"
                    outlined
                    suffix="days"
                  ></v-text-field>
                </v-col>
                <v-col>
                  <h2 class="text-center">Shore & Yard Crane Assumptions</h2>
                  <v-text-field
                    label="Share Crane Workhour/Year"
                    outlined
                    suffix="%"
                    @click:append="
                      shareCraneWorkHourShow = !shareCraneWorkHourShow
                    "
                    :append-icon="
                      shareCraneWorkHourShow ? 'mdi-eye' : 'mdi-eye-off'
                    "
                    :type="shareCraneWorkHourShow ? 'text' : 'password'"
                  ></v-text-field>
                  <v-text-field
                    label="Yard Crane Workhour/Year"
                    outlined
                    suffix="%"
                    @click:append="
                      yardCraneWorkHourShow = !yardCraneWorkHourShow
                    "
                    :append-icon="
                      yardCraneWorkHourShow ? 'mdi-eye' : 'mdi-eye-off'
                    "
                    :type="yardCraneWorkHourShow ? 'text' : 'password'"
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card>

          <v-btn color="primary" @click="routerParams += 1"> Next </v-btn>
          <v-btn text @click="routerParams -= 1"> Back </v-btn>
        </v-stepper-content>

        <v-stepper-content step="4">
          <v-card elevation="0" class="mb-12">
            <chart :chartId="'target'" :chartData="targetChartData" />
          </v-card>

          <v-btn color="primary" @click="routerParams += 1"> Next </v-btn>
          <v-btn text @click="routerParams = 1"> Back </v-btn>
        </v-stepper-content>

        <v-stepper-content step="5">
          <v-card class="mb-12" elevation="0">
            <v-container>
              <v-row>
                <v-col>
                  <h1>Target Container Terminal Capacity (TEUS)</h1>
                  <h4 class="text-center">
                    To increase your container terminal capacity
                  </h4>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <v-text-field
                    label="From"
                    outlined
                    suffix="TEU/Year"
                  ></v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                    label="To"
                    outlined
                    suffix="TEU/Year"
                  ></v-text-field>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <h3>With your current state, you may need to:</h3>
                  <ul>
                    <li>Increase your quay lenght by 100 meter</li>
                    <li>Increase your effective yard capacty by 5.000</li>
                    <li>Add 1 Shore Crane</li>
                    <li>Add 2 RTG</li>
                    <li>Add 6 Internal Truck</li>
                  </ul>
                  <p>
                    Please remember to do the financial and commercial
                    feasibility study before take your decision
                  </p>
                </v-col>
              </v-row>
            </v-container>
          </v-card>

          <v-btn color="primary" @click="routerParams += 1"> Next </v-btn>
          <v-btn text @click="routerParams = 1"> Back </v-btn>
        </v-stepper-content>

        <v-stepper-content step="6">
          <v-card class="mb-12" elevation="0">
            <v-container>
              <h1>Man Power Assumptions</h1>
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
                  <div class="d-flex justify-space-between">
                    <h3 class="man-power-assumption">
                      Yard Operator Assistant (OA)
                    </h3>
                    <v-radio-group v-model="row" row>
                      <v-radio label="No" value="radio-1"></v-radio>
                      <v-radio label="Yes" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between">
                    <h3 class="man-power-assumption">SC Operator</h3>
                    <v-radio-group v-model="row" row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between">
                    <h3 class="man-power-assumption">Solo</h3>
                    <v-radio-group v-model="row" row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between">
                    <h3 class="man-power-assumption">Whisky</h3>
                    <v-radio-group v-model="row" row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between">
                    <h3 class="man-power-assumption">YC Operator</h3>
                    <v-radio-group v-model="row" row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between">
                    <h3 class="man-power-assumption">Yard OA</h3>
                    <v-radio-group v-model="row" row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between">
                    <h3 class="man-power-assumption">ITT Operator</h3>
                    <v-radio-group v-model="row" row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between">
                    <h3 class="man-power-assumption">Gate Officer</h3>
                    <v-radio-group v-model="row" row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between">
                    <h3 class="man-power-assumption">Gate Inspector</h3>
                    <v-radio-group v-model="row" row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between">
                    <h3 class="man-power-assumption">Traffic Man</h3>
                    <v-radio-group v-model="row" row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                  <div class="d-flex justify-space-between">
                    <h3 class="man-power-assumption">Planner</h3>
                    <v-radio-group v-model="row" row>
                      <v-radio label="Permanent" value="radio-1"></v-radio>
                      <v-radio label="Contract" value="radio-2"></v-radio>
                    </v-radio-group>
                  </div>
                </v-col>
              </v-row>
            </v-container>

            <v-container>
              <h1>Equipment Assumptions</h1>
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
                  <h1>Operation Cost Impact Estimation</h1>
                  <div id="manpower-cost" class="my-6">
                    <h3>Manpower Cost Gap Estimation / Year</h3>
                    <v-text-field label="Cost Gap" outlined suffix="Rupiah">
                      <template v-slot:append-outer>
                        <v-btn color="secondary">See Detail</v-btn>
                      </template>
                    </v-text-field>
                  </div>

                  <div id="fuel-cost" class="my-6">
                    <h3>Fuel Cost Gap Estimation / Year</h3>
                    <v-text-field label="Cost Gap" outlined suffix="Rupiah">
                      <template v-slot:append-outer>
                        <v-btn color="secondary">See Detail</v-btn>
                      </template>
                    </v-text-field>
                  </div>
                </v-col>
              </v-row>
            </v-container>
          </v-card>

          <v-btn color="primary" @click="routerParams += 1"> Next </v-btn>
          <v-btn text @click="routerParams = 1"> Back </v-btn>
        </v-stepper-content>

        <v-stepper-content step="7">
          <v-card class="mb-12" elevation="0">
            <v-container>
              <h1>Equipment Assumptions</h1>
              <h3>Investment Cost</h3>
              <v-row>
                <v-col>
                  <v-text-field
                    label="QCC"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="HMC"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Reach Stacker"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Permanent Employee Salary"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Slide Loader"
                    outlined
                    suffix="Rp/group"
                  ></v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                    label="RTGC"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="RMGC"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Internal Truck"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Slide Loader"
                    outlined
                    suffix="Rp/group"
                  ></v-text-field>
                </v-col>
              </v-row>

              <v-divider></v-divider>

              <v-row>
                <v-col>
                  <h3>Yard Assumptions</h3>
                  <v-text-field
                    label="Tier Max in Storage Yard"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Stacking Area / yard area"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Berth Wide"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Pavement type"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                  <v-text-field
                    label="Investment Cost / m2"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                </v-col>
                <v-col>
                  <h3>Berth Assumptions</h3>
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
                        suffix="Rp/m2"
                      ></v-text-field>
                    </v-col>
                  </v-row>

                  <h3>Gate Assumptions</h3>
                  <v-row>
                    <v-col>
                      <v-text-field
                        label="Inv cost / m2 (Gate In)"
                        outlined
                        suffix="Rp/m2"
                      ></v-text-field>
                    </v-col>
                    <v-col>
                      <v-text-field
                        label="Inv cost / m2 (Gate Out)"
                        outlined
                        suffix="Rp/m2"
                      ></v-text-field>
                    </v-col>
                  </v-row>

                  <h3>Weighing Scale</h3>
                  <v-row>
                    <v-col>
                      <v-text-field
                        label="Inv cost / m2 (Gate In)"
                        outlined
                        suffix="Rp/m2"
                      ></v-text-field>
                    </v-col>
                  </v-row>
                </v-col>
              </v-row>

              <v-divider></v-divider>

              <h3>IT Infrastructure Assumptions</h3>
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
                    label="Equipment (Control Tower)"
                    outlined
                    suffix="Rp/Unit"
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-container>

            <v-container>
              <h1>Investment Cost Impact Estimation Due To Improvements</h1>

              <h3>Equiment</h3>
              <v-row>
                <v-col>
                  <div>
                    <v-text-field
                      label="1 HMC, 2 RTG, 6 ITT"
                      outlined
                      suffix="Rupiah"
                    >
                      <template v-slot:append-outer>
                        <v-btn color="secondary">See Detail</v-btn>
                      </template>
                    </v-text-field>
                  </div>
                </v-col>
              </v-row>

              <h3>Facility</h3>
              <v-row>
                <v-col>
                  <v-text-field label="Yard" outlined suffix="Rupiah">
                    <template v-slot:append-outer>
                      <v-btn color="secondary">See Detail</v-btn>
                    </template>
                  </v-text-field>

                  <v-text-field label="Berth" outlined suffix="Rupiah">
                    <template v-slot:append-outer>
                      <v-btn color="secondary">See Detail</v-btn>
                    </template>
                  </v-text-field>

                  <v-text-field label="Gate" outlined suffix="Rupiah">
                    <template v-slot:append-outer>
                      <v-btn color="secondary">See Detail</v-btn>
                    </template>
                  </v-text-field>

                  <v-text-field
                    label="IT Infrastructure"
                    outlined
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
          <v-btn color="primary" @click="routerParams += 1"> Next </v-btn>
          <v-btn text @click="routerParams = 1"> Back </v-btn>
        </v-stepper-content>

        <v-stepper-content step="8">
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
          <v-btn color="primary" @click="completed()"> Complete </v-btn>
          <v-btn text @click="routerParams = 1"> Back </v-btn>
        </v-stepper-content>
      </v-stepper-items>
    </v-stepper>
  </div>
</template>

<script>
import Chart from '@/components/Chart'

export default {
  components: { Chart },
  data: () => ({
    e1: 1,
    targetChartData: {
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
    currentChartData: {
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
          label: 'Existing Container Terminal Capacity (TEUS)',
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
    teuShow: true,
    shareCraneWorkHourShow: true,
    yardCraneWorkHourShow: true,
  }),
  methods: {
    completed() {
      console.log("yes!");
    },
  },
  computed: {
    routerParams: {
      get: function () {
        return parseInt(this.$route.query.id)
      },
      set: function (args) {
        return this.$router.push({ path: this.$route.path, query: { id: args }})
      }
    },
  },
};
</script>

<style scoped>
.v-text-field__suffix {
  color: 375.804;
}
h1,
h3,
h2 {
  padding: 5px;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
  margin-bottom: 10px;
  color: white;
}
h3.man-power-assumption {
  color: black;
}
h3,
h3:not(".man-power-assumption") h2 {
  background-color: #30ccfd;
}
h1 {
  background-color: #0e2d61;
}
h4 {
  color: #30ccfd;
}
</style>