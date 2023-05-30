<template>
  <div class="profile-main">
    <div class="container">
      <div class="style-border">
        <h1>ข้อมูลผู้ใช้งาน</h1>
        <div class="menu-search" role="search">
          <input
            class="form-control me-2"
            type="search"
            placeholder="Search"
            aria-label="Search"
            v-model="searchText"
            @input="handleSearch"
          />
          <button
            class="btn btn-outline-success"
            type="submit"
            @click="handleSearch"
          >
            Search
          </button>
        </div>
        <div class="main-profile">
          <div class="mt-2">Number Of User : {{ profile.length }}</div>
          <div v-if="profile.length > 0">
            <div
              class="data-profile"
              v-for="(x, n) of profile"
              :key="'profile' + n"
            >
              <!-- {{ x }} -->
              <div class="row">
                <div class="col-md-9">
                  <div class="data-profile-content">
                    <div>name : {{ x.name }}</div>
                    <div>birthdate : {{ x.birthdate }}</div>
                    <div>address : {{ x.address }}</div>
                    <div>user : {{ x.user }}</div>
                    <!-- <div>password : {{ x.password }}</div> -->
                  </div>
                </div>
                <div class="col-md-3 m-auto">
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
          </div>
          <div v-else>No Data</div>

          <div class="row justify-content-center" v-if="isEdit">
            <div class="input-data-main">
              <div class="header-add-edit">
                <h2>แก้ไขข้อมมูล</h2>
              </div>
              <div class="input-data-content">
                <input type="text" v-model="profileData.name" />
              </div>
              <div class="input-data-content">
                <input
                  class="input-date"
                  type="date"
                  v-model="profileData.birthdate"
                />
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
              <div>
                <button class="button-add-comtent" @click="addData">
                  Update
                </button>
              </div>
            </div>
          </div>
          <div class="row justify-content-center" v-else>
            <div class="input-data-main">
              <div class="header-add-edit">
                <h2>เพิ่มข้อมูล</h2>
              </div>
              <div class="input-data-content">
                <input
                  type="text"
                  placeholder="name"
                  v-model="profileData.name"
                />
              </div>
              <div class="input-data-content">
                <input
                  class="input-date"
                  type="date"
                  v-model="profileData.birthdate"
                />
              </div>
              <div class="input-data-content">
                <input
                  type="textarea"
                  placeholder="address"
                  v-model="profileData.address"
                />
              </div>
              <div class="input-data-content">
                <input
                  type="text"
                  placeholder="user"
                  v-model="profileData.user"
                />
              </div>
              <div class="input-data-content">
                <input
                  type="password"
                  placeholder="password"
                  v-model="profileData.password"
                />
              </div>
              <div>
                <button class="button-add-comtent" @click="addData">
                  Add User
                </button>
              </div>
            </div>
          </div>
        </div>
        <!-- <button
          type="button"
          class="btn btn-primary"
          data-bs-toggle="modal"
          data-bs-target="#exampleModal"
        >
          Launch demo modal
        </button> -->

        <!-- Modal -->
        <div
          class="modal fade"
          id="exampleModal"
          tabindex="-1"
          aria-labelledby="exampleModalLabel"
          aria-hidden="true"
        >
          <div class="modal-dialog">
            <div class="modal-content">
              <div class="modal-header">
                <h1 class="modal-title fs-5" id="exampleModalLabel">
                  Modal title
                </h1>
                <button
                  type="button"
                  class="btn-close"
                  data-bs-dismiss="modal"
                  aria-label="Close"
                ></button>
              </div>
              <div class="modal-body">...</div>
              <div class="modal-footer">
                <button
                  type="button"
                  class="btn btn-secondary"
                  data-bs-dismiss="modal"
                >
                  Close
                </button>
                <button type="button" class="btn btn-primary">
                  Save changes
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, Ref } from "vue";
import Profile from "../assets/infomation.json";

interface profileModal {
  name: string;
  birthdate: string;
  address: string;
  user: string;
  password: string;
}
export default defineComponent({
  name: "profile",
  setup() {
    var profile: Ref<profileModal[]> = ref(Profile);
    var profileClone: Ref<profileModal[]> = ref(Profile);

    var profileIndex: Ref<number | null> = ref(null);
    var isEdit = ref(false);
    var searchText = ref("");
    var message = ref("");
    var profileData = ref({
      name: "",
      birthdate: "",
      address: "",
      user: "",
      password: "",
    });

    function addData() {
      if (profileIndex.value != null) {
        profileIndex.value = null;
        profileClone.value[profileIndex?.value || 0] = profileData.value;
        return (profile.value[profileIndex?.value || 0] = profileData.value);
      }
      profile.value.push(profileData.value);
      profileClone.value.push(profileData.value);
      isEdit.value = false;
      profileData.value = {
        name: "",
        birthdate: "",
        address: "",
        user: "",
        password: "",
      };
    }
    function editProfile(index: number, x: profileModal) {
      isEdit.value = true;
      profileData.value = { ...x };
      profileIndex.value = index;
    }
    function deleteProfile(n: any) {
      profile.value.splice(n, 1);
    }
    function handleSearch() {
      if (searchText.value === "") {
        return (profile.value = profileClone.value);
      }
      let result = profile.value.filter((el) =>
        el.name
          .toLocaleLowerCase()
          .includes(searchText.value.toLocaleLowerCase())
      );
      profile.value = result;
    }
    return {
      profile,
      profileIndex,
      isEdit,
      profileData,
      addData,
      editProfile,
      deleteProfile,
      searchText,
      handleSearch,
    };
  },
});
</script>

<style lang="scss">
@media only screen and (max-width: 600px) {
  .sidebar-main {
    text-align: start;
  }
  
  .data-profile {
    font-size: 13px;
  }
  .button-edit-main {
    margin: 10px 0;
  }
  .input-data-main {
    width: 100% !important;
  }
  .style-border{
    padding: 0.5rem !important;
  }
  .menu-search {
    width: 100% !important;
  }
  
}
.profile-main {
  color: white;
  background-color: #1c1e21;
  min-height: calc(100vh - 56px);
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
        margin: 10px 0;
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
  
  .button-add-comtent {
    width: 100px;
    border-radius: 15px;
    background: #31a24c;
    color: rgb(255, 255, 255);
  }
  .input-data-main {
    background-color: #18191a;
    width: 350px;
    padding: 1.5rem;
    border-radius: 15px;
    margin: 1rem 0;
    .input-data-content {
      margin: 0.5rem 0;
    }
    .input-date {
      width: 228px;
    }
  }
  .menu-search {
    display: flex;
    width: 50%;
    margin: auto;
  }
  
  
}
</style>
