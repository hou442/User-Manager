<template>
    <div class="customers container">
        <Alert v-if="alert" :message="alert"></Alert>
        <h1 class="page-header">用户管理系统</h1>
        <input class="form-control" type="text" v-model="filterInput" placeholder="搜索"/>
        <table class="table table-striped">
            <thead>
                <tr>
                    <th>姓名</th>
                    <th>电话</th>
                    <th>邮箱</th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="customer in filterBy(customers,filterInput)">
                    <td>{{customer.name}}</td>
                    <td>{{customer.phone}}</td>
                    <td>{{customer.email}}</td>
                    <td><router-link class="btn btn-default" v-bind:to="'/customer/'+customer.id">详情</router-link></td>
                </tr>
            </tbody>
        </table>

    </div>
</template>

<script>
// import func from '../../vue-temp/vue-editor-bridge';
import Alert from './Alert' 
export default {
    name:'customers',
    data(){
        return{
            customers:[],
            alert:"",
            filterInput:""
        }
    },
    components:{
        Alert
    },
    methods:{
        fetchCustomers(){
            this.$http.get("http://localhost:3000/users")
            .then(function(res){
                // console.log(res);
                this.customers = res.body;
            })
        },
        filterBy(customers,value){
            return customers.filter(customer=>{
                return customer.name.match(value);
            })
        }
    },
    created(){
        if(this.$route.query.alert){
            this.alert = this.$route.query.alert;
        }
        this.fetchCustomers()
    },
    updated(){
        this.fetchCustomers()
    }
}
</script>

<style>

</style>