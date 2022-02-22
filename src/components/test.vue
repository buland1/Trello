<template>
  <div>
    <v-row>
      <!----- Step 1 Creating an Issue Card--->
      <v-col md="4">
        <div id="issue">
          <v-card class="mx-auto" max-width="330">
            <v-card-text>
              <div><b>Issues</b></div>
            </v-card-text>

            <!--Inserting values in the card-->
            <v-row>
              <v-col cols="6" sm="12">
                <v-card
                  height="150px"
                  class="mb-2 pa-2"
                  color="#385F73"
                  dark
                  v-for="(value, index) in issueList"
                  :key="index"
                >
                  <v-card-title class="blue white--text">
                    <span> {{ value.issueStatus }} </span>

                    <v-spacer></v-spacer>

                    <v-menu bottom left>
                      <template v-slot:activator="{ on, attrs }">
                        <v-btn dark icon v-bind="attrs" v-on="on">
                          <v-icon>mdi-dots-vertical</v-icon>
                        </v-btn>
                      </template>

                      <v-list>
                        <v-list-item
                          v-for="(item, x) in itemsArrow"
                          :key="x"
                          @click="clickArrow({ cardIndex: index, moveTo: x })"
                        >
                          <v-list-item-title>{{
                            item.title
                          }}</v-list-item-title>
                        </v-list-item>
                      </v-list>
                    </v-menu>
                  </v-card-title>

                  <v-card-text
                    ><h3
                      class="white--text align-left pt-2"
                      style="text-align: left"
                    >
                      {{ value.issueDescription }}
                    </h3></v-card-text
                  >
                </v-card>
              </v-col>
            </v-row>

            <!---- Step 4 Creating Add Issue Button-------->
            <v-card-actions>
              <v-btn block color="purple" dark @click="dialog = true">
                <v-icon dark left>mdi-plus-circle </v-icon> Add New Issue
              </v-btn>
            </v-card-actions>
          </v-card>
        </div>
      </v-col>

      <!-----Step 2 Creating a Processing Card--->
      <v-col md="4">
        <v-card class="mx-auto" max-width="330">
          <v-card-text>
            <div><b>On Progress</b></div>
          </v-card-text>

          <v-row>
            <v-col cols="6" sm="12">
              <v-card
                height="150px"
                class="mb-2 pa-2"
                color="#385F73"
                dark
                v-for="(value, index) in onProgressList"
                :key="index"
              >
                <v-card-title class="blue white--text">
                  <span> {{ value.issueStatus }} </span>

                  <v-spacer></v-spacer>

                  <v-menu bottom left>
                    <template v-slot:activator="{ on, attrs }">
                      <v-btn dark icon v-bind="attrs" v-on="on">
                        <v-icon>mdi-dots-vertical</v-icon>
                      </v-btn>
                    </template>

                    <v-list>
                      <v-list-item
                        v-for="(item, y) in itemsArrow2"
                        :key="y"
                        @click="clickArrow1({ cardIndex: index, moveTo: y })"
                      >
                        <v-list-item-title>{{ item.title }}</v-list-item-title>
                      </v-list-item>
                    </v-list>
                  </v-menu>
                </v-card-title>

                <v-card-text
                  ><h3
                    class="white--text align-left pt-2"
                    style="text-align: left"
                  >
                    {{ value.issueDescription }}
                  </h3></v-card-text
                >
              </v-card>
            </v-col>
          </v-row>
        </v-card>
      </v-col>

      <!-----Step 3 Creating a Completed Card--->
      <v-col md="4">
        <v-card class="mx-auto" max-width="330">
          <v-card-text>
            <div><b>Completed and Closed</b></div>
          </v-card-text>
          <v-row>
            <v-col cols="6" sm="12">
              <v-card
                height="150px"
                class="mb-2 pa-2"
                color="#385F73"
                dark
                v-for="(value, index) in completedList"
                :key="index"
              >
                <v-card-title class="blue white--text">
                  <span> {{ value.issueStatus }} </span>

                  <v-spacer></v-spacer>

                  <v-menu bottom left>
                    <template v-slot:activator="{ on, attrs }">
                      <v-btn dark icon v-bind="attrs" v-on="on">
                        <v-icon>mdi-dots-vertical</v-icon>
                      </v-btn>
                    </template>

                    <v-list>
                      <v-list-item
                        v-for="(item, z) in itemsArrow3"
                        :key="z"
                        @click="clickArrow2({ cardIndex: index, moveTo: z })"
                      >
                        <v-list-item-title>{{ item.title }}</v-list-item-title>
                      </v-list-item>
                    </v-list>
                  </v-menu>
                </v-card-title>

                <v-card-text
                  ><h3
                    class="white--text align-left pt-2"
                    style="text-align: left"
                  >
                    {{ value.issueDescription }}
                  </h3></v-card-text
                >
              </v-card>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>

    <!---- Step 5 Creating a dialog box----->
    <v-dialog v-model="dialog" persistent max-width="400px">
      <v-card>
        <!---Diaogue Title --->
        <v-card-title>
          <span class="text-h5">Issue List</span>
        </v-card-title>
        <!---Diaogue Text Areas --->
        <v-card-text>
          <v-col class="d-flex" cols="6" sm="6">
            <v-select
              :items="items"
              label="Status"
              v-model="status"
              dense
              solo
            ></v-select>
          </v-col>
          <v-col cols="12" md="12">
            <v-textarea
              outlined
              name="input-7-4"
              label="Description"
              v-model="description"
              value=""
            ></v-textarea>
          </v-col>
        </v-card-text>

        <!---Diaogue Actions --->
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="clearField(0)">
            Clear
          </v-btn>
          <v-btn color="blue darken-1" text @click="clearField(1)">
            Close
          </v-btn>
          <v-btn color="blue darken-1" text @click="saveField()"> Save </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>
        

<script>
export default {
  name: "Test",
  data: () => ({
    status: "",
    description: "",
    dialog: false,
    issueList: [],
    onProgressList: [],
    completedList: [],
    items: ["Critical", "Major", "Minor", "Urgent", "Others"],
    itemsArrow: [
      { title: "Move to On Processing" },
      { title: "Move to Completed and Closed" },
    ],
    itemsArrow2: [
      { title: "Move to Issue List" },
      { title: "Move to Completed and Closed" },
    ],
    itemsArrow3: [
      { title: "Move to Issue List" },
      { title: "Move to On Progress" },
    ],
  }),

  mounted() {
    this.issueLocalStorage();
    this.progressLocalStorage();
    this.completedStorage();
  },

  // All types of functions are created in a methods
  methods: {
    clearField(status) {
      if (status == 1) this.dialog = false; // Passing a parameter to close a dialog box
      this.status = "";
      this.description = "";
    },
    // closeField() {
    //   this.dialog = false;
    //   this.status="";
    //   this.description="";
    // },
    saveField() {
      let fetchIssueList = localStorage.getItem("issueList"); // get data from local storage
      if (fetchIssueList === null) {
        // console.log("if");
        //checks whether the data is present in local storage or not
        //JSON.stringify => Converts JavaScript Object or value to a JSON string

        //syntax ==> localStorage.setItem(keyname, value): keyname= issueList and value= json.stingify
        localStorage.setItem(
          "issueList",
          JSON.stringify([
            {
              issueStatus: this.status,
              issueDescription: this.description,
            },
          ])
        );
      } else {
        fetchIssueList = JSON.parse(fetchIssueList); // retreiving to the object
        fetchIssueList.push({
          issueStatus: this.status,
          issueDescription: this.description,
        });
        localStorage.setItem("issueList", JSON.stringify(fetchIssueList));
      }
      this.clearField(1);
      this.issueLocalStorage();
    },
    issueLocalStorage() {
      let issueStorage = localStorage.getItem("issueList");
      if (issueStorage) {
        this.issueList = JSON.parse(issueStorage);
      }
    },
    clickArrow({ cardIndex, moveTo }) {
      if (moveTo === 0) {
        let onProgressList = this.issueList.splice(cardIndex, 1);
        let OnProgress = localStorage.getItem("onProgressList");
        if (OnProgress === null) {
          localStorage.setItem(
            "onProgressList",
            JSON.stringify(onProgressList)
          );
          // console.log(onProgressList, "here...");
        } else {
          OnProgress = JSON.parse(OnProgress);
          OnProgress.push(onProgressList[0]);
          localStorage.setItem("onProgressList", JSON.stringify(OnProgress));
        }
        this.progressLocalStorage();
        localStorage.setItem("issueList", JSON.stringify(this.issueList));
      } else {
        let completedList = this.issueList.splice(cardIndex, 1);
        let completeCase1 = localStorage.getItem("completedList");
        if (completeCase1 === null) {
          localStorage.setItem("completedList", JSON.stringify(completedList));
          console.log(completedList, "here...");
        } else {
          completeCase1 = JSON.parse(completeCase1);
          completeCase1.push(completedList[0]);
          localStorage.setItem("completedList", JSON.stringify(completeCase1));
        }
        this.completedStorage();
        localStorage.setItem("issueList", JSON.stringify(this.issueList));
      }
    },
    clickArrow1({ cardIndex, moveTo }) {
      if (moveTo === 0) {
        let issueList = this.onProgressList.splice(cardIndex, 1);
        let proIssue = localStorage.getItem("issueList");
        // console.log("gethere", proIssue,issueList)
        console.log(proIssue, issueList);
        // if (proIssue === null || this.issueList.length===0)
        if (proIssue === null) {
          localStorage.setItem("issueList", JSON.stringify(issueList));
          console.log("here", proIssue);
        } else {
          proIssue = JSON.parse(proIssue);
          proIssue.push(issueList[0]);
          localStorage.setItem("issueList", JSON.stringify(proIssue));
          console.log("there", proIssue);
        }
        this.issueLocalStorage();
        localStorage.setItem(
          "onProgressList",
          JSON.stringify(this.onProgressList)
        );
      } else {
        let completedList = this.onProgressList.splice(cardIndex, 1);
        let completeCase = localStorage.getItem("completedList");
        if (completeCase === null) {
          localStorage.setItem("completedList", JSON.stringify(completedList));
          console.log(completedList, "here...");
        } else {
          completeCase = JSON.parse(completeCase);
          completeCase.push(completedList[0]);
          localStorage.setItem("completedList", JSON.stringify(completeCase));
        }
        this.completedStorage();
        localStorage.setItem(
          "onProgressList",
          JSON.stringify(this.onProgressList)
        );
      }
    },
    clickArrow2({ cardIndex, moveTo }) {
      if (moveTo === 0) {
        let issueList = this.completedList.splice(cardIndex, 1);
        let proIssue = localStorage.getItem("issueList");
        console.log(proIssue, issueList);
        // if (proIssue === null || this.issueList.length===0)
        if (proIssue === null) {
          localStorage.setItem("issueList", JSON.stringify(issueList));
          console.log("here", proIssue);
        } else {
          proIssue = JSON.parse(proIssue);
          proIssue.push(issueList[0]);
          localStorage.setItem("issueList", JSON.stringify(proIssue));
          console.log("there", proIssue);
        }
        this.issueLocalStorage();
        localStorage.setItem(
          "completedList",
          JSON.stringify(this.completedList)
        );
      } else {
        let onProgressList = this.completedList.splice(cardIndex, 1);
        let OnProgress = localStorage.getItem("onProgressList");
        if (OnProgress === null) {
          localStorage.setItem(
            "onProgressList",
            JSON.stringify(onProgressList)
          );
        } else {
          OnProgress = JSON.parse(OnProgress);
          OnProgress.push(onProgressList[0]);
          localStorage.setItem("onProgressList", JSON.stringify(OnProgress));
        }
        this.progressLocalStorage();
        localStorage.setItem(
          "completedList",
          JSON.stringify(this.completedList)
        );
      }
    },

    progressLocalStorage() {
      let progressStorage = localStorage.getItem("onProgressList");
      if (progressStorage) {
        this.onProgressList = JSON.parse(progressStorage);
      }
    },
    completedStorage() {
      let completedStorage = localStorage.getItem("completedList");
      if (completedStorage) {
        this.completedList = JSON.parse(completedStorage);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
</style>