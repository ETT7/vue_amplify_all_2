<template>
  <div class="app-body">
    <div class="card-container">
      <div class="name">{{ userData.email }}</div>
      <div class="symbol">{{ userData.lotnumber }}</div>
    </div>
  </div>
</template>

<script>
import { API, graphqlOperation } from "aws-amplify";
import { Auth } from "aws-amplify";
import { getUser } from "../graphql/queries";
export default {
  data() {
    return {
      user: {},
      tasks: [],
      form: {},

      userData: [],
    };
  },
  computed: {
    sortedUsers() {
      let users = [...this.userData];
      return users;
    },
  },
  created() {
    // authentication state managament

    this.getData();

    // Auth.currentAuthenticatedUser({
    //   bypassCache: false, // Optional, By default is false. If set to true, this call will send a request to Cognito to get the latest user data
    // })
    //   .then((user) => this.user={...user})
    //   .catch((err) => console.log(err));

    //Subscribe to changes
  },
  methods: {
    async getData() {
      let user = await Auth.currentAuthenticatedUser();
      const { attributes } = user;
      const { sub } = attributes;
      console.log("hehhehe", sub);
      try {
        const response = await API.graphql(
          graphqlOperation(getUser, { id: sub })
        );
        this.userData = response.data.getUser;
        console.log("hahaha", response);
      } catch (error) {
        console.log("Error loading Users...", error);
      }
    },
  },
};
</script>
