<template>
  <div>
    <v-row>
      <!----- Step 1 Creating an Issue Card--->
      <v-col md="4">
        <div id="issue">
          <v-card class="mx-auto" max-width="330">
            <v-card-text>
              <div id="issueHere"><b>Issues</b></div>
            </v-card-text>

            <!--Inserting values in the card-->
            <v-row>
              <v-col cols="6" sm="12">
                <draggable
                  class="issue-list-group"
                  group="people"
                  @end="onEnd"
                  @drag="clickArrow({ cardIndex: index, moveTo: x })"
                >
                  <v-card
                    :list="issueList"
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
                </draggable>
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
            <div id="progresHere"><b>On Progress</b></div>
          </v-card-text>
          <v-row>
            <v-col cols="6" sm="12">
              <draggable
                class="onprogress-list-group"
                group="people"
                @end="onEnd"
                cardIndex:index
                @drag="clickArrow1({ cardIndex: index, moveTo: y })"
              >
                <!-- @end="onEnd" -->
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
              </draggable>
            </v-col>
          </v-row>
        </v-card>
      </v-col>

      <!-----Step 3 Creating a Completed Card--->
      <v-col md="4">
        <v-card class="mx-auto" max-width="330">
          <v-card-text>
            <div id="closedHere"><b>Completed and Closed</b></div>
          </v-card-text>
          <v-row>
            <v-col cols="6" sm="12">
              <draggable
                class="closed-list-group"
                group="people"
                @end="onEnd"
                @drag="clickArrow2({ cardIndex: index, moveTo: x })"
              >
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
              </draggable>
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
import draggable from "vuedraggable";
export default {
  name: "Test",
  components: {
    draggable,
  },
  data: () => ({
    status: "",
    description: "",
    dialog: false,
    draggable: true,
    issueList: [],
    // hellIssue: [],
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

  methods: {
    clearField(status) {
      if (status == 1) this.dialog = false;
      this.status = "";
      this.description = "";
    },
    closeField() {
      this.dialog = false;
      this.status = "";
      this.description = "";
    },
    saveField() {
      let fetchIssueList = localStorage.getItem("issueList");
      if (fetchIssueList === null || !fetchIssueList) {
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
    onEnd(e) {
      const fromClass = e.from.className;
      const oldIndex = e.oldIndex;

      const toClass = e.to.className;
      // const newIndex = e.newIndex;

      let movedElement = null;
      console.log(movedElement);

      let removeFromSection = "";

      if (fromClass === "issue-list-group") {
        removeFromSection = "issueList";
      } else if (fromClass === "onprogress-list-group") {
        removeFromSection = "onProgressList";
      } else if (fromClass === "closed-list-group") {
        removeFromSection = "completedList";
      } else {
        console.log("Sorry this time");
      }

      let hellIssue = localStorage.getItem(removeFromSection);
      hellIssue = JSON.parse(hellIssue);
      movedElement = hellIssue.splice(oldIndex, 1);
      movedElement = movedElement[0];
      localStorage.setItem(removeFromSection, JSON.stringify(hellIssue));

      let getToSection = "";
      if (toClass === "issue-list-group") {
        getToSection = "issueList";
      } else if (toClass === "onprogress-list-group") {
        getToSection = "onProgressList";
      } else if (toClass === "closed-list-group") {
        getToSection = "completedList";
      } else {
        console.log("Sorry this time");
      }

        let hellProgress = localStorage.getItem(getToSection);
        hellProgress = JSON.parse(hellProgress);
        if (hellProgress === null || !hellProgress) {
          localStorage.setItem(
            getToSection,
            JSON.stringify([movedElement])
          );
        } else {
          hellProgress.push(movedElement);
          localStorage.setItem(getToSection, JSON.stringify(hellProgress));
        }
        console.log(getToSection)
      // if (toClass === "onprogress-list-group") {
      //   let hellProgress = localStorage.getItem("onProgressList");
      //   hellProgress = JSON.parse(hellProgress);
      //   if (hellProgress === null || !hellProgress) {
      //     localStorage.setItem(
      //       "onProgressList",
      //       JSON.stringify([movedElement])
      //     );
      //   } else {
      //     hellProgress.push(movedElement);
      //     localStorage.setItem("onProgressList", JSON.stringify(hellProgress));
      //   }
      // } else if (toClass === "closed-list-group") {
      //   let hellClosed = localStorage.getItem("completedList");
      //   hellClosed = JSON.parse(hellClosed);
      //   if (hellClosed === null || !hellClosed) {
      //     localStorage.setItem("completedList", JSON.stringify([movedElement]));
      //   } else {
      //     hellClosed.push(movedElement);
      //     localStorage.setItem("completedList", JSON.stringify(hellClosed));
      //   }
      // } else if (toClass === "issue-list-group") {
      //   let hellIssue = localStorage.getItem("issueList");
      //   hellIssue = JSON.parse(hellIssue);
      //   if (hellIssue === null || !hellIssue) {
      //     localStorage.setItem("issueList", JSON.stringify([movedElement]));
      //   } else {
      //     hellIssue.push(movedElement);
      //     localStorage.setItem("issueList", JSON.stringify(hellIssue));
      //   }
      // } else {
      //   console.log("Are you doing things correctly??");
      // }
    },
  },
};
</script>

<style>
.issue-list-group {
  min-height: 20px;
}

.onprogress-list-group {
  min-height: 100px;
}
.closed-list-group {
  min-height: 100px;
}
</style>