<template>
  <div>
    <v-row>
      <v-col md="4">
        <div id="issue">
          <v-card class="mx-auto" max-width="330">
            <v-card-text>
              <div><b>Issues</b></div>
            </v-card-text>
            <v-card class="mx-auto" max-width="auto" max-height="auto">
              <v-card-text>
                <!-- <v-col cols="6" md ="12">
                  <v-textarea label="" value=""></v-textarea>
                </v-col> -->
                <v-card
                  class="mb-2 pa-2"
                  color="#385F73"
                  dark
                  v-for="(value, index) in issue_list"
                  :key="index"
                >
                  <!-- <v-card-title padding-bottom> {{ value.issueCase }}</v-card-title> -->
                  <v-card class="text-sm-left pa-2 mb-2">{{value.issueCase}} </v-card>
                  <p class="text-sm-left">{{ value.issuedesc }}</p>
                  <!-- <p color="#385F73" dark align="left">Description</p> -->

                  <!-- <v-card-subtitle class="text-h10">Description</v-card-subtitle> -->
                </v-card>
              </v-card-text>
              <!-- {{ issue_list }} -->
            </v-card>
            <v-card-actions>
              <v-btn color="success" @click="dialog = true" block id="addbtn">
                Create New Issue
              </v-btn>
            </v-card-actions>
          </v-card>
        </div>
      </v-col>
      <v-col>
         <div id = "onProgress">
        <v-card class="mx-auto" max-width="330">
          <v-card-text>
            <div><b>On Progress</b></div>
          </v-card-text>
        </v-card>
         </div>
      </v-col> 

      <v-col>
         <div id = "closed">
        <v-card class="mx-auto" max-width="330">
          <v-card-text>
            <div><b>Completed and Closed</b></div>
          </v-card-text>
        </v-card>
         </div>
      </v-col> 
    </v-row>
    <!--dialog box---->
    <v-dialog v-model="dialog" persistent max-width="500px">
      <v-card>
        <v-card-title class="primary white--text">
          <span class="title">Issue List</span>
        </v-card-title>
        <v-card-text>
          <v-row>
            <v-col sm="12">
              <v-select
                :items="['Critical', 'Minor', 'Major', 'Others']"
                label="Issue"
                v-model="status"
              ></v-select>
            </v-col>
            <v-col sm="12">
              <v-container fluid>
                <v-textarea
                  name="input-7-1"
                  filled
                  label="Description"
                  auto-grow
                  v-model="description"
                ></v-textarea>
              </v-container>
            </v-col>
          </v-row>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="warning" outlined @click="clearField()">Close</v-btn>
          <v-btn color="success" outlined @click="save()">Save</v-btn>
          <v-btn color="black" text @click="clearFieldSet()">Clear</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <!---dialog box--->
  </div>
</template>

<script>
export default {
  name: "Abc",
  // created(){
  //   this.save()
  //   console.log("Created lifeCycle Hook is Created")
  // },
  data: () => ({
    status: "",
    description: "",
    dialog: false,
    issue_list: [],
  }),

  mounted() {
    this.fetchIssuesLS();
  },

  methods: {
    save() {
      /**
       * 1) Fetch Local storage saved issue list
       * 2) If Yes ->
       *    1)  parse old local storage value to js object (should become array)
       *    2)  add new item to this array
       *    3)  now save this new array to local storage
       * 3) If No -> Save this value to local storage as array
       */

      let fetchIssuesList = localStorage.getItem("issue_list");

      if (fetchIssuesList === null) {
        //stringify object and store
        localStorage.setItem(
          "issue_list",
          JSON.stringify([
            {
              issueCase: this.status,
              issuedesc: this.description,
            },
          ])
        );

        // No
      } else {
        fetchIssuesList = JSON.parse(fetchIssuesList); //retrieve the object
        fetchIssuesList.push({
          issueCase: this.status,
          issuedesc: this.description,
        });
        localStorage.setItem("issue_list", JSON.stringify(fetchIssuesList));
      }
      this.clearField();
      this.fetchIssuesLS();
    },
    clearField() {
      this.dialog = false; //convert to parameter
      this.status = "";
      this.description = "";
    },
    clearFieldSet() {
      this.status = "";
      this.description = "";
    },
    fetchIssuesLS() {
      let issuesList = localStorage.getItem("issue_list");
      if (issuesList) {
        this.issue_list = JSON.parse(issuesList);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
</style>