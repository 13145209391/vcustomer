<template>
  <div class="customerdetails container">
		<router-link to="/" class="btn btn-default btn-sm">返回</router-link>
    <h1 class="page-header">
			<span class="glyphicon glyphicon-user"></span>  {{customer.name}}
			<span class="pull-right">
				<router-link class="btn btn-primary btn-sm" v-bind:to="'/edit/' + customer.id">编辑</router-link>
				<button class="btn btn-danger btn-sm" @click="deleteCustomer(customer.id)">删除</button>
			</span>
		</h1>
    <ul class="list-group">
			<li class="list-group-item"><span class="glyphicon glyphicon-hand-right"> 性别:  {{customer.sex}}</span></li>
			<li class="list-group-item"><span class="glyphicon glyphicon-hand-right"> 年龄:  {{customer.age}}</span></li>
      <li class="list-group-item"><span class="glyphicon glyphicon-hand-right"> 手机:  {{customer.phone}}</span></li>
      <li class="list-group-item"><span class="glyphicon glyphicon-hand-right"> 邮箱:  {{customer.email}}</span></li>
    </ul>
		<ul class="list-group">
			<li class="list-group-item"><span class="glyphicon glyphicon-hand-right"> 学历:  {{customer.education}}</span></li>
			<li class="list-group-item"><span class="glyphicon glyphicon-hand-right"> 学校:  {{customer.school}}</span></li>
			<li class="list-group-item"><span class="glyphicon glyphicon-hand-right"> 职业:  {{customer.profession}}</span></li>
			<li class="list-group-item"><span class="glyphicon glyphicon-hand-right"> 简介:  {{customer.profile}}</span></li>
		</ul>
  </div>
</template>

<script>
export default {
  name: 'customerdetails',
  data () {
    return {
       customer:""
    }
  },
  methods:{
    fetchCustomer(id){
      this.$http.get("http://localhost:3000/users/"+ id)
          .then( response => {
              //console.log(response)
              this.customer = response.body;
          })
    },
		deleteCustomer(id){
			 this.$http.delete("http://localhost:3000/users/"+ id)
			     .then(function(){
						 this.$router.push({path:"/",query:{alert:"用户删除成功！"}})
					 })
		}
  },
  created(){
    this.fetchCustomer(this.$route.params.id)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
