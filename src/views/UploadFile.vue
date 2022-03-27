<template>
  <div class="container">
    <div class="large-12 medium-12 small-12 cell">
      <label
        >File
        <input
          type="file"
          id="file"
          ref="file"
          v-on:change="handleFileUpload()"
        />
      </label>
      <button v-on:click="submitFile()">Submit</button>
    </div>
  </div>
</template>

<script>
import { createTask } from "../graphql/mutations";

import { API, graphqlOperation } from "aws-amplify";
export default {
  data() {
    return {
      file: "",
      csvData: {},
    };
  },

  created() {
    // authentication state managament
    //Subscribe to changes
  },

  methods: {
    /*
        Submits the file to the server
      */
    async submitFile() {
      this.$papa.parse(this.file, {
        header: true,
        skipEmptyLines: true,
        complete: async function (results) {
          this.csvData = results.data;

          for (const item of this.csvData) {
            let taskName = item.taskName;
            let details = item.details;
            console.log("color", item);
            const task = { taskName, details, clientId: this.clientId };
            try {
              const response = await API.graphql(
                graphqlOperation(createTask, { input: task })
              );
              console.log("Item created!");
              console.log(response);
            } catch (error) {
              console.log("Error creating task...", error);
            }
          }
        },
      });
    },

    /*
        Handles a change on the file upload
      */
    handleFileUpload() {
      this.file = this.$refs.file.files[0];
    },
  },
};
</script>
