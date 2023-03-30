<template>
  <div>
    <h1 class="red text-center">Student Details</h1>
    <div class="manTable">
      <table width="100%">
        <td>
          <div class="text-center">
            <router-link :to="{ name: 'addNewStudent' }">
              <v-btn rounded color="primary" dark> Add New Student </v-btn>
            </router-link>
          </div>
        </td>

        <!-- <td>
          <v-btn class="red" @click="getData">show student Details</v-btn>
        </td> -->
      </table>
    </div>

    <!-- <v-data-table :headers="headers" :items="users" :search="search" class="elevation-1">
    <template v-slot:item="{ item }">
      <v-list-item-content>
        <v-list-item-title class="text-h6">{{ item.fname }}</v-list-item-title>
        <v-list-item-subtitle>{{ item.lmail }}</v-list-item-subtitle>
        <v-list-item-subtitle>{{ item.email }}</v-list-item-subtitle>
        <v-list-item-subtitle>{{ item.course }}</v-list-item-subtitle>
        <v-list-item-subtitle>{{ item.gender }}</v-list-item-subtitle>
        <v-list-item-subtitle>{{ item.address }}</v-list-item-subtitle>
        <v-list-item-subtitle>{{ item.phone }}</v-list-item-subtitle>
      </v-list-item-content>

      <td>{{ item.fname }}</td>
      <td>{{ item.lname }}</td>
      <td>{{ item.email }}</td>
      <td>{{ item.course }}</td>
       <td>{{ item.gender }}</td> 
       <td>{{ item.address }}</td> 
      <td>{{ item.phone }}</td>


     
    </template>
  </v-data-table> -->

    <template>
      <v-table fixed-header height="300px" v-show="showTable">
        <thead>
          <tr>
            <th class="text-left" width="100px">Id</th>
            <th class="text-left" width="150px">FirstName</th>
            <th class="text-left" width="170px">Lastname</th>
            <th class="text-left" width="280px">Email</th>
            <th class="text-left" width="100px">Course</th>
            <th class="text-left" width="170px">tel</th>
            <th class="text-left" width="170px">update/remove</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in users" :key="item.id" height="50px">
            <td>{{ item.id }}</td>
            <td>{{ item.fname }}</td>
            <td>{{ item.lname }}</td>
            <td>{{ item.email }}</td>
            <td>{{ item.course }}</td>
            <td>{{ item.phone }}</td>
            <td>
              <v-icon  class="mr-2" @click="editUser(item.id)"
                >mdi-pencil</v-icon
              >
              <v-icon @click="deleteUser(item.id)">mdi-delete</v-icon>
            </td>
          </tr>
        </tbody>
      </v-table>
    </template>
  </div>
</template>

<script>
import axios from "axios";
import router from "@/router/index";

export default {
  // name:'StudentDetails',

  data() {
    return {
      headers: [
        { text: "Id", value: "id" },
        { text: "Fname", value: "fname" },
        { text: "Lname", value: "lname" },
        { text: "Email", value: "email" },
        { text: "Course", value: "course" },
        // { text: 'Gender', value: 'gender' },
        // { text: 'Address', value: 'address' },
        { text: "Phone", value: "phone" },
      ],
      users: [],
      search: "",
      showTable: false,
    };
  },

  methods: {
    getData() {
      (this.showTable = !this.showTable),
        console.log(
          "Data was successfully retrieved from the JSON Server endpoint!"
        );
      axios
        .get("http://localhost:3000/users")
        .then((response) => {
          console.log(response.data);
          this.users = response.data;
          //console.log("fname")
          //console.log(this.users[0].email)
        })
        .catch((error) => {
          console.error(
            "An error occurred while retrieving data from the JSON Server endpoint."
          );
          console.log(error);
        });
    },

    editUser(id) {
      console.log(id);
      //router.push('/AddNewStudent');
      router.push({ name: "addNewStudent", params: { id: id } });
    },

    async deleteUser(id) {
      try {
        const response = await fetch(`http://localhost:3000/users/${id}`, {
          method: "DELETE",
        });
        if (response.ok) {
          const index = this.users.findIndex((user) => user.id === id);
          if (index !== -1) {
            this.users.splice(index, 1);
          }
          alert("User deleted successfully");
        } else {
          throw new Error("Failed to delete user");
        }
      } catch (error) {
        console.error(error);
        alert("Failed to delete user");
      }
    },
  },

  mounted(){
    this.getData()
  }
};
</script>



<style>
.manTable {
  padding: 100px;
}
</style>
