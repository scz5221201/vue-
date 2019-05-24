<template>
  <div class="Add container">
    <h1 class="page-header">添加用户</h1>
    <form v-on:submit="addCustomers">
      <div class="well">
        <h4>用户信息</h4>
        <div class="form-group">
          <label>姓名</label>
          <input type="text" class="form-control" placeholder="姓名" v-model="customer.name">
        </div>
        <div class="form-group">
          <label>电话</label>
          <input type="text" class="form-control" placeholder="电话" v-model="customer.phone">
        </div>
        <div class="form-group">
          <label>邮箱</label>
          <input type="text" class="form-control" placeholder="邮箱" v-model="customer.email">
        </div>
        <div class="form-group">
          <label>学历</label>
          <input type="text" class="form-control" placeholder="学历" v-model="customer.education">
        </div>
        <div class="form-group">
          <label>毕业学校</label>
          <input
            type="text"
            class="form-control"
            placeholder="毕业学校"
            v-model="customer.graduationSchool"
          >
        </div>
        <div class="form-group">
          <label>职业</label>
          <input type="text" class="form-control" placeholder="职业" v-model="customer.profession">
        </div>
        <div class="form-group">
          <label>个人简介</label>
          <textarea class="form-control" rows="10" v-model="customer.profile"></textarea>
        </div>
        <button type="submit">确定</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Add',
  data() {
    return {
      customer: {}
    }
  },
  methods: {
    addCustomers(e) {
      if (!this.customer.name || !this.customer.phone || !this.customer.email) {
        alert("请输入对应的信息")
      } else {
        let newCustomer = {
          name: this.customer.name,
          phone: this.customer.phone,
          email: this.customer.email,
          education: this.customer.education,
          graduationSchool: this.customer.graduationSchool,
          profession: this.customer.profession,
          profile: this.customer.profile
        }
        this.$http.post("http://localhost:3000/user", newCustomer)
          .then(function (response) {

            this.$router.push({ path: "/", query: { alertInfo: "用户信息添加成功" } })
          })
        e.preventDefault();
      }
      e.preventDefault();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
