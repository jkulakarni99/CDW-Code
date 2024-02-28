<template>
  <div class="header">
    <div class="content-wrapper">
      <span class="header-text">Team</span>
      <div class="input-icons">
        <span class="mdi mdi-account-search icon"></span>
        <input
          v-model="searchText"
          id="searchInput"
          type="text"
          class="input-field"
          @keyup="onEnter"
          placeholder="Search"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HeaderComponent',
  data: () => ({
    searchText: ''
  }),
  methods: {
    onEnter(e) {
      this.searchText = e.target.value
      if (e.keyCode === 13 || !this.searchText) this.doSearch()
    },
    doSearch() {
      this.$emit('doFilter', this.searchText)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  height: 80px;
  width: 100vw;
  top: 0;
  background-color: #6d9eed;
  display: flex;
  align-items: center;
  position: fixed;
}
.content-wrapper {
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 0 2rem;
}
.header-text {
  color: #fff;
  font-size: 2rem;
  font-weight: bold;
}
.input-field {
  height: 40px;
  width: 300px;
  border-radius: 20px;
  padding: 0 3rem;
  border: none;
  margin-top: 5px;
  font-size: 1.3rem;
}
.input-field:focus-visible {
  outline: none
}
.input-icons span {
  position: absolute;
}
.icon {
  margin-left: 1rem;
  font-size: 2rem;
}
</style>
