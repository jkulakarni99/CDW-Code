<template>
  <div class="adminstrators">
    <div class="section-header">{{ header }}</div>
    <div class="user-wrapper" v-if="userList.length > 0">
      <div class="user-card" v-for="(item, index) in userList" :key="index" >
        <img class="avatar" :src="item.img" />
        <div class="user-info">
          <span>{{item.first_name}} {{item.last_name}}</span>
          <p>{{item.email}}</p>
        </div>
      </div>
      </div>
      <div v-else class="empty-msg">
        <div class="err-header">Opps, No {{header}} found !!!!</div> 
        <div>Please refresh the page or clear the filter to get the list.</div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'UserList',
  props: {
    header: String,
    userList: Array,
  },
  
  data: () => ({
    listOfUsers: []
  }),
  created() {
    this.listOfUsers = this.userList
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p {
  margin: 0;
  padding: 0;
  font-size: 13px;
  font-weight: 500;
  color: #808080;
}
.user-wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  margin: 0 2rem 2rem 2rem;
}
.user-card {
  border-radius: 10px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  margin: 1rem;
  height: 90px;
  display: flex;
  align-items: center;
  padding-left: 1rem;
  cursor: pointer;
  transition: all .1s ease-in-out;
}
.user-card:hover {
  transform: scale(1.1);
}
.avatar {
  border-radius: 50%;
  width: 70px;
  height: 70px;
}
.user-info {
  margin-left: 1rem;
  display: flex;
  flex-direction: column;
  font-size: 20px;
  font-weight: 600;
}
.section-header {
  margin-left: 3rem;
  font-size: 1.5rem;
  font-weight: 600;
  color: #808080
}
.empty-msg {
  margin: 2rem 3rem 3rem 3rem; 
}
.err-header {
  color: #ce1126;
  font-weight: 600;
  font-size: 1.5rem;
}
</style>
