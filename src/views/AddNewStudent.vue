<template>
  <div>
    <template>
  <v-form @submit.prevent="chooseBetween">
    <v-container>
      <v-toolbar color="primary" dark>
        <v-toolbar-title>Student Registration Form</v-toolbar-title>
      </v-toolbar>
      <hr />

      <v-row>
        <v-col cols="12" md="6">
          <v-text-field
            label="Firstname"
            name="firstname"
            required
            v-model="firstname"
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="6">
          <v-text-field
            label="Lastname"
            name="lastname"
            required
            v-model="lastname"
          ></v-text-field>
        </v-col>

        <v-col cols="12">
          <label>Course:</label>
          <select v-model="course">
            <option disabled value="">Course</option>
            <option value="SE">SE</option>
            <option value="QA">QA</option>
            <option value="BA">BA</option>
          </select>
        </v-col>

        <v-col cols="12">
          <label>Gender:</label><br />
          <input type="radio" value="Male" name="gender" checked v-model="gender" />
          Male
          <input type="radio" value="Female" name="gender" v-model="gender" />
          Female
          <input type="radio" value="Other" name="gender" v-model="gender" />
          Other
        </v-col>

        <v-col cols="12" md="6">
          <v-text-field
            label="Phone"
            name="phone"
            required
            v-model="phone"
          ></v-text-field>
        </v-col>

        <v-col cols="12">
          <label>Current Address:</label>
          <textarea
            cols="50"
            rows="3"
            placeholder="Current Address"
            required
            v-model="address"
          >
          </textarea>
        </v-col>

        <v-col cols="12">
          <v-text-field
            label="Email"
            name="email"
            required
            v-model="email"
          ></v-text-field>
        </v-col>

        <v-col cols="12">
          <v-btn color="primary" dark @click="chooseBetween">Register</v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
</template>

    <DialogAlert
      ref="dialog"
      :operation="operation"
      :description="description"
    ></DialogAlert>
  </div>
</template>

<script>
import axios from "axios";
import DialogAlert from '../components/DialogAlert.vue';

export default {
  components: {
    DialogAlert,
  },

  data() {
    return {
      firstname: "",
      lastname: "",
      course: "",
      gender: "",
      phone: "",
      address: "",
      email: "",

      id: "",
      users: [],
      toogleUpdate: false,
      datas: [],
      operation: "sucessfull",
      description: "operation sucessfull",
    };
  },
  methods: {
    openDialog() {
      this.$refs.dialog.dialogVisible = true;
    },
    chooseBetween() {
      if (this.toogleUpdate) {
        this.register();
        console.log("register data selected ");
      } else {
        this.update();
        console.log("update data selected ");
      }
    },

    update() {
      console.log("update ");
      const data = {
        fname: this.firstname,
        lname: this.lastname,
        course: this.course,
        gender: this.gender,
        phone: this.phone,
        address: this.address,
        email: this.email,
        id: this.id,
      };
      //console.log(data.fname)

      axios
        .put(`http://localhost:3000/users/${data.id}`, data)
        .then((response) => {
          console.log(response.data);
          // alert("user updated successfully")
          this.openDialog();
        })
        .catch((error) => {
          if (error.response.status === 404) {
            console.log("Requested resource not found.");
          }
          console.log(error);
        });
    },

    register() {
      console.log(this.firstname), console.log(this.lastname);

      const users = {
        fname: this.firstname,
        lname: this.lastname,
        course: this.course,
        gender: this.gender,
        phone: this.phone,
        address: this.address,
        email: this.email,
      };
      console.log(users.fname);

      axios
        .post("http://localhost:3000/users", users)
        .then((response) => {
          console.log(
            "Data was successfully written to the JSON Server endpoint!"
          );
          //this.dialog=true
          console.log(response.data); // The data that was written to the endpoint
          this.openDialog();

          this.firstname = "";
          this.lastname = "";
          this.course = "";
          this.gender = "";
          this.phone = "";
          this.address = "";
          this.email = "";
        })
        .catch((error) => {
          console.error(
            "An error occurred while writing data to the JSON Server endpoint."
          );
          console.error(error);
        });
    },

    getUserById(id) {
      (this.toogleUpdate = !this.toogleUpdate),
        axios
          .get(`http://localhost:3000/users/${id}`)
          .then((response) => {
            const user = response.data;
            this.users.push(user);
            this.firstname = user.fname;
            this.lastname = user.lname;
            this.course = user.course;
            this.gender = user.gender;
            this.phone = user.phone;
            this.address = user.address;
            this.email = user.email;
          })
          .catch((error) => {
            console.log(error);
          });
    },
  },

  mounted() {
    (this.id = this.$route.params.id), console.log("student id");
    console.log(this.id);
    this.getUserById(this.id);
  },
};
</script>

<style scoped>
form {
  max-width: 700px;
  margin: 30px auto;
  background: rgb(236, 235, 235);
}
.container {
  padding: 50px;
  /* background-color: rgb(63, 64, 65);   */
}

input[type="text"],
input[type="password"],
textarea {
  width: 100%;
  padding: 15px;
  margin: 5px 0 22px 0;
  display: inline-block;
  border: none;
  background: #f1f1f1;
}
input[type="text"]:focus,
input[type="password"]:focus {
  background-color: rgb(223, 247, 247);
  outline: none;
}
div {
  padding: 10px 0;
}
hr {
  border: 1px solid #f1f1f1;
  margin-bottom: 25px;
}
.registerbtn {
  background-color: #889e89;
  color: white;
  padding: 16px 20px;
  margin: 8px 0;
  border: none;
  cursor: pointer;
  width: 100%;
  opacity: 0.9;
}
.registerbtn:hover {
  opacity: 1;
}
</style>
