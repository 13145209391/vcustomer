<template>
  <div class="customers container">
    <Alert v-if="alert" v-bind:message="alert"></Alert>
    <h1 class="page-header">用户管理系统</h1>
    <table class="table table-striped">
       <thead>
         <tr>
           <th>姓名</th>
					 <th>性别</th>
					 <th>年龄</th>
           <th>手机</th>
           <th>邮箱</th>
           <th></th>
         </tr>
       </thead>
       <tbody>
           <tr v-for="customer in customers" :key="customer.id">
             <td>{{customer.name}}</td>
						 <td>{{customer.sex}}</td>
						 <td>{{customer.age}}</td>
             <td>{{customer.phone}}</td>
             <td>{{customer.email}}</td>
             <td><router-link class="btn btn-default btn-sm" v-bind:to="'/customer/' + customer.id">详情</router-link></td>
           </tr>
         </tbody>
    </table>
  </div>
</template>

<script>
import Alert from "./Alert";
export default {
  name: 'customers',
  data () {
    return {
        customers:[],
        alert:""
    }
  },
  methods:{
    fetchCustomer(){
      this.$http.get("http://localhost:3000/users")
          .then( response => {
              //console.log(response)
              this.customers = response.body;
          })
    }
  },
  created(){
    if(this.$route.query.alert){
      this.alert = this.$route.query.alert;
    }
    this.fetchCustomer();
  },
  updated(){
    this.fetchCustomer();
  },
  components:{
    Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
