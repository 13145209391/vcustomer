<template>
    <div class="customers container">
        <Alert v-if="alert" v-bind:message="alert"></Alert>
        <h1 class="page-header">用户管理系统</h1>
        <input type="text" class="form-control" placeholder="搜索" v-model="fifleterInput">
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
                <tr v-for="customer in filterList" :key="customer.id">
                    <td>{{customer.name}}</td>
                    <td>{{customer.sex}}</td>
                    <td>{{customer.age}}</td>
                    <td>{{customer.phone}}</td>
                    <td>{{customer.email}}</td>
                    <td>
                        <router-link class="btn btn-default btn-sm" v-bind:to="'/customer/' + customer.id">详情</router-link>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    import Alert from "./Alert";
    export default {
        name: 'customers',
        data() {
            return {
                customers: [],
                alert: "",
                fifleterInput: ""
            }
        },
        methods: {
            fetchCustomer() {
                this.axios.get("http://localhost:3000/users")
                    .then(response => {
                        //console.log(response)
                        this.customers = response.data;
                    })
            },
            filterBy(customers, value) {
                return customers.filter(customer => {
					return Object.values(customer).find(v => (v+'').match(value));
                })
            }
        },
        computed: {
            filterList() {
                return this.filterBy(this.customers, this.fifleterInput);
            }
        },
        created() {
            if (this.$route.query.alert) {
                this.alert = this.$route.query.alert;
            }
            this.fetchCustomer();
        },
		/*watch: {
			fifleterInput(newVal) {
				this.fetchCustomer();
			}
		},*/
        components: {
            Alert
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
