<template>
  <div class="container">
    <div class="style-border">
      <div class="main-profile">
        <div class="icon-profile"><img src="" alt="" /></div>
        <!-- <div class="name">{{ profile }}</div> -->
        <div
          v-for="(x, n) of profile"
          :key="'profile' + n"
          style="background-color: red; padding: 10px 5px; margin: 10px 0"
        >
          <!-- {{ x }} -->
          <div>name : {{ x.name }}</div>
          <div>birthdate : {{ x.birthdate }}</div>
          <div @click="editProfile(n, x)">edit</div>
          <div @click="deleteProfile(n)">delete</div>
        </div>
        <div class="row" v-if="isEdit">
          <div class="col-12">
            <input type="text" v-model="profileData.name" />
          </div>
          <div class="col-12">
            <input type="date" v-model="profileData.birthdate" />
          </div>
          <div class="col-12">
            <input type="textarea" v-model="profileData.address" />
          </div>
          <div class="col-12">
            <input type="text" v-model="profileData.user" />
          </div>
          <div class="col-12">
            <input type="password" v-model="profileData.password" />
          </div>
          <div><button @click="addData">Add User</button></div>
        </div>
        <div class="row" v-else>
          <div class="col-12">
            <input type="text" v-model="profileData.name" />
          </div>
          <div class="col-12">
            <input type="date" v-model="profileData.birthdate" />
          </div>
          <div class="col-12">
            <input type="textarea" v-model="profileData.address" />
          </div>
          <div class="col-12">
            <input type="text" v-model="profileData.user" />
          </div>
          <div class="col-12">
            <input type="password" v-model="profileData.password" />
          </div>
          <div><button @click="addData">Add User</button></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Profile from "../assets/infomation.json";
export default {
  data() {
    return {
      profile: Profile,
      profileData: {
        name: "",
        birthdate: "",
        address: "",
        user: "",
        password: "",
      },
      isEdit: false,
      profileIndex: null,
    };
  },
  methods: {
    addData() {
      console.log(this.profileIndex);
      if (this.profileIndex != null) {
        return (this.profile[this.profileIndex] = this.profileData);
      }
      this.profile.push(this.profileData);
    },
    editProfile(index, x) {
      this.isEdit = true;
      this.profileData = { ...x };
      this.profileIndex = index;
    },
    deleteProfile(n) {
      this.profile.splice(n, 1);
    },
  },
};
</script>

<style lang="scss">
.style-border {
  border: 1px solid red;
}
</style>