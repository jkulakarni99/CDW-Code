<template>
  <div id="app">
    <HeaderComponent @doFilter="applyFilter"/>
    <UserList header="Administrators" :userList="adminList" style="margin-top: 7rem"/>
    <div class="divider"></div>
    <UserList class="user-list" header="Members" :userList="memberList" />
    <button class="add-button"><span class="mdi mdi-plus add-icon"></span></button>
  </div>
</template>

<script>
import UserList from './components/UsersToDisplay.vue'
import HeaderComponent from './components/HeaderComponent.vue'
export default {
  name: 'App',
  components: {
    UserList,
    HeaderComponent,
  },
  data: () => ({
    allList: [],
    adminList: [],
    memberList: [],
    showAdmin: false,
  }),
  methods: {
    async getAndformatAdminsMembers() {
      const data = await fetch("https://mocki.io/v1/ddb7e0a8-e218-4e36-b1be-b902cdb1c098");
      const json = await data.json();
      this.allList = json;
      console.log(this.allList);
      this.adminList = json.filter(ele => ele.role.toLowerCase() === 'admin');
      this.memberList = json.filter(ele => ele.role.toLowerCase() === 'member');
    },
    applyFilter(val) {
      const filteredArr = this.allList.reduce((acc, cur) => {
        let present = false;
        Object.keys(cur).forEach(key => {
          if ((key === 'first_name' || key === 'last_name' || key === 'email') && cur[key].toLowerCase()
          .includes(val.toLowerCase())) present = true;
        });
        if (present) acc.push(cur);
        return acc
      }, []);
      this.adminList = filteredArr.filter(ele => ele.role.toLowerCase() === 'admin');
      this.memberList = filteredArr.filter(ele => ele.role.toLowerCase() === 'member');
    }
  },
  created() {
    this.getAndformatAdminsMembers();
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: 'Poppins'
}
.user-list {
  margin-top: 3rem;
}
.divider {
  border: 1px solid #808080;
  margin: 3rem
}
.add-button {
  position: fixed;
  right: 6rem;
  top: 90vh;
  border-radius: 50%;
  height: 60px;
  width: 60px;
  border: none;
  background: #6d9eed;
}
.add-icon {
  font-size: 2rem;
  font-weight: 600;
  color: #fff
}
</style>
