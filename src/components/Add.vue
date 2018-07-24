<template>
  <div class="add container">
		<Alert v-if="alert" v-bind:message="alert"></Alert>
     <h1 class="page-header">添加用户</h1>   
     <form v-on:submit="addCustomer">
         <div class="well">
           <h4>用户信息</h4>
           <div class="form-group">
               <label for="">姓名</label>
               <input type="text" class="form-control" placeholder="Name" v-model="customer.name">
           </div>
					 <div class="form-group">
							<label for="">性别</label>
							<div class="dropdown">
								<select name="" id="" class="btn btn-default dropdown-toggle" style="width: 100%;" v-model="customer.sex">
									<option value="男">男</option>
									<option value="女">女</option>
								</select>
							</div>
					 </div>
					 <div class="form-group">
					 		<label for="">年龄</label>
					 		<input type="text" class="form-control" placeholder="Age" v-model="customer.age">
					 </div>
           <div class="form-group">
               <label for="">手机</label>
               <input type="text" class="form-control" placeholder="Phone" v-model="customer.phone">
           </div>
           <div class="form-group">
               <label for="">邮箱</label>
               <input type="text" class="form-control" placeholder="Email" v-model="customer.email">
           </div>
           <div class="form-group">
               <label for="">学历</label>
               <input type="text" class="form-control" placeholder="Education" v-model="customer.education">
           </div>
           <div class="form-group">
               <label for="">毕业学校</label>
               <input type="text" class="form-control" placeholder="School" v-model="customer.school">
           </div>
           <div class="form-group">
               <label for="">职业</label>
               <input type="text" class="form-control" placeholder="Profession" v-model="customer.profession">
           </div>
           <div class="form-group">
               <label for="">个人简介</label>
               <textarea type="textarea" class="form-control" placeholder="Profile" v-model="customer.profile"></textarea>
           </div>
           <button type="submit" class="btn btn-primary">添加</button>
           
         </div>
     </form>
  </div>
</template>

<script>
import Alert from './Alert'
export default {
  name: 'add',
  data () {
    return {
        customer:{},
				alert:""
    }
  },
  methods:{
      addCustomer(e){
          if(!this.customer.name || !this.customer.sex ||!this.customer.age ||!this.customer.phone ||!this.customer.email){
               this.alert = "请添加对应姓名、性别、年龄、电话、邮箱的信息"
          }else{
              let newCustomer = {
                  name : this.customer.name,
									sex : this.customer.sex,
									age : this.customer.age,
                  phone : this.customer.phone,
                  email : this.customer.email,
                  education : this.customer.education,
                  school : this.customer.school,
                  profession : this.customer.profession,
                  profile : this.customer.profile,
              }
              this.axios.post("http://localhost:3000/users",newCustomer)
                  .then( response=>{
                      //console.log(response)
                      this.$router.push({path:"/",query:{alert:"用户添加信息成功!"}});
                  })
                  e.preventDefault();
          }
          e.preventDefault();
      }
  },
	components:{
		Alert
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
