<template>
  <div>
    <h1 class="mx-auto" style="width: 100px">Users</h1>
    <div class="wrapper mx-auto">
      <input
        style="border: 1px solid black"
        type="text"
        placeholder="Ism familiya"
        v-model="inputName"
      />
      <input
        style="border: 1px solid black"
        type="text"
        placeholder="Login"
        v-model="inputLogin"
      />
      <input
        style="border: 1px solid black"
        type="text"
        placeholder="Tel"
        v-model="inputTel"
      />
      <input
        type="text"
        style="border: 1px solid black"
        placeholder="Parol"
        v-model="inputParol"
      />
      <button class="success add-btn" style="padding: 2px" @click="addNewUser">
        Qo'shish
      </button>
    </div>
    <div class="mx-auto" style="width: 300px">
      <p>{{ message }}</p>
    </div>
    <div class="mx-auto" style="width: 1200px">
      <table>
        <tr>
          <th>ID</th>
          <th>FISh</th>
          <th>Login</th>
          <th>Tel</th>
          <th>Parol</th>
          <th>Amallar</th>
        </tr>
        <tr v-for="(user, index) in users" :key="index">
          <td>{{ user.id }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.login }}</td>
          <td>{{ user.tel }}</td>
          <td>{{ user.parol }}</td>
          <td>
            <button class="delete" @click="deleteUser(index)">delete</button>
            <button class="edit" @click="editUser(index)">edit</button>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>
<script>
import { breaking } from "vuetify/lib/util/console";

export default {
  data() {
    return {
      message: "",
      userId: "",
      inputName: "",
      inputLogin: "",
      inputTel: "",
      inputParol: "",
      users: [
        {
          id: 1,
          name: "Rasulov Sanjarbek",
          login: "rasulov",
          tel: "2030344",
          parol: "12345678",
        },
      ],
    };
  },
  methods: {
    addNewUser() {
      const btn = document.querySelector(".add-btn");
      if (
        this.inputName == "" ||
        this.inputLogin == "" ||
        this.inputTel == "" ||
        this.inputParol == ""
      ) {
        btn.classList.remove("success");
        this.message = "Barcha inputlar toldirilishi shart";
      } else if (this.inputParol.length < 8) {
        btn.classList.remove("success");
        this.message = "Parol 8ta belgidan kam bolmasligi kerak";
      } else {
        btn.classList.add("success");
        this.message = "";
        const indexUser = this.users.findIndex(
          (user) => user.id === this.userId
        );
        if (indexUser === -1) {
          let uniqueLogin = this.users.filter(
            (user) => user.login === this.inputLogin
          );
          let uniqueTel = this.users.filter(
            (user) => user.tel === this.inputTel
          );
          // this.users.filter((user) => {
          //   if (user.tel === this.inputTel) {
          //     this.message = "Bu raqam oldin ishlatilgan";
          //   }
          // });
          if (uniqueLogin.length === 0 && uniqueTel.length === 0) {
            this.users.push({
              id: this.users.length + 1,
              name: this.inputName,
              login: this.inputLogin,
              tel: this.inputTel,
              parol: this.inputParol,
            });
            (this.inputName = ""),
              (this.inputLogin = ""),
              (this.inputTel = ""),
              (this.inputParol = "");
          } else {
            btn.classList.remove("success");
            this.message = "Ushbu raqam yoki login mavjud";
          }
        } else {
          let uniqueLogin = this.users.filter(
            (user) => user.login === this.inputLogin
          );
          if (uniqueLogin.length === 0) {
            this.users.splice(indexUser, 1, {
              id: this.userId,
              name: this.inputName,
              login: this.inputLogin,
              tel: this.inputTel,
              parol: this.inputParol,
            });
            (this.inputName = ""),
              (this.inputLogin = ""),
              (this.inputTel = ""),
              (this.inputParol = "");
          } else if (
            uniqueLogin.length > 0 &&
            uniqueLogin[0].id === this.userId
          ) {
            this.users.splice(indexUser, 1, {
              id: this.userId,
              name: this.inputName,
              login: this.inputLogin,
              tel: this.inputTel,
              parol: this.inputParol,
            });
            (this.inputName = ""),
              (this.inputLogin = ""),
              (this.inputTel = ""),
              (this.inputParol = "");
          } else {
            this.message = "Ushbu login mavjud";
          }
        }
      }
    },
    deleteUser(index) {
      this.users.splice(index, 1);
    },
    editUser(index) {
      this.userId = this.users[index].id;
      this.inputName = this.users[index].name;
      this.inputLogin = this.users[index].login;
      this.inputTel = this.users[index].tel;
      this.inputParol = this.users[index].parol;
    },
  },
};
</script>

<style>
input {
  padding: 5px;
}

th {
  width: 200px;
}

tr {
  width: 200px;
  text-align: center;
}

.delete {
  border: 1px solid black;
  background-color: red;
  color: white;
  margin-right: 5px;
}

.edit {
  border: 1px solid black;
  background-color: dimgrey;
  color: white;
}

.wrapper {
  max-width: 950px;
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}
</style>
