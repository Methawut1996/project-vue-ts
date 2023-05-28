<template>
  <div class="profile-main">
    <div class="container">
      <div class="style-border">
        <h1>ข้อมูลผู้ใช้งาน</h1>
        <div class="main-profile">
          <!-- <div class="name">{{ profile }}</div> -->
          <div
            class="data-profile"
            v-for="(x, n) of profile"
            :key="'profile' + n"
          >
            <!-- {{ x }} -->
            <div class="row">
              <div class="col-9">
                <div class="data-profile-content">
                  <div>name : {{ x.name }}</div>
                  <div>birthdate : {{ x.birthdate }}</div>
                  <div>address : {{ x.address }}</div>
                  <div>user : {{ x.user }}</div>
                  <div>password : {{ x.password }}</div>
                </div>
              </div>
              <div class="col-3 m-auto">
                <div class="button-edit-main">
                  <button class="button-edit-content">
                    <div @click="editProfile(n, x)">edit</div>
                  </button>
                  <button class="button-delete-content">
                    <div @click="deleteProfile(n)">delete</div>
                  </button>
                </div>
              </div>
            </div>
          </div>

          <div class="row justify-content-center" v-if="isEdit">
            <div class="input-data-main">
            <div class="input-data-content">
              <input type="text" v-model="profileData.name" />
            </div>
            <div class="input-data-content">
              <input class="input-date" type="date" v-model="profileData.birthdate" />
            </div>
            <div class="input-data-content">
              <input type="textarea" v-model="profileData.address" />
            </div>
            <div class="input-data-content">
              <input type="text" v-model="profileData.user" />
            </div>
            <div class="input-data-content">
              <input type="password" v-model="profileData.password" />
            </div>
            <div><button @click="addData">Add User</button></div>
          </div>
        </div>
          <div class="row justify-content-center" v-else>
            <div class="input-data-main">
            <div class="input-data-content">
              <input type="text" placeholder="name" v-model="profileData.name"/>
            </div>
            <div class="input-data-content ">
              <input class="input-date" type="date" v-model="profileData.birthdate" />
            </div>
            <div class="input-data-content">
              <input type="textarea" placeholder="address" v-model="profileData.address" />
            </div>
            <div class="input-data-content">
              <input type="text" placeholder="user" v-model="profileData.user" />
            </div>
            <div class="input-data-content">
              <input type="password" placeholder="password" v-model="profileData.password" />
            </div>
            <div><button class="button-add-comtent" @click="addData">Add User</button></div>
          </div>
        </div>
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
.profile-main {
  color: white;
  background-color: #1c1e21;
  h1 {
    color: white;
    margin: 1rem 0;
  }
  .style-border {
    padding: 1.5rem;
  }
  .data-profile {
    background-color: #18191a;
    padding: 1rem 1.5rem;
    margin: 10px 0;
    color: white;
    border-radius: 10px;
    .data-profile-content {
      text-align: start;
    }
    .button-edit-main {
      button {
        width: 80px;
        margin: 0 0.25rem;
        border-radius: 15px;
      }
      .button-edit-content {
        background: bottom;
        div {
          color: white;
        }
      }
      .button-delete-content {
        background: rgb(255, 50, 50);
        div {
          color: white;
        }
      }
    }
  }
  .button-add-comtent{
    width: 100px;
    border-radius: 15px;
    background: #31a24c;
    color:rgb(255, 255, 255);
  }
  .input-data-main{
    background-color: #18191a;
    width: 35%;
    padding: 1.5rem;
    border-radius: 15px;
    margin: 1rem 0;
    .input-data-content{
    margin: 0.5rem 0;
  }
  .input-date{
    width: 228px;
  }
  }
  
}
</style>
