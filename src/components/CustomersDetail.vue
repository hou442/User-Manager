<template>
    <div class="about container">
        <router-link class="btn btn-default" to="/ ">返回</router-link>
        <h1 class="page-header">
            {{customer.name}}
            <span class="pull-right">
                <router-link class="btn btn-primary" :to="'/edit/'+customer.id">编辑</router-link>
                <button class="btn btn-danger" @click="deleteCustomer(customer.id)">删除</button>
            </span>
        </h1>
        <ul class="list-group">
            <li class="list-group-item"><span class="glyphicon glyphicon-phone">{{customer.phone}}</span></li>
            <li class="list-group-item"><span class="glyphicon glyphicon-envelope">{{customer.email}}</span></li>
        </ul>
        <ul class="list-group">
            <li class="list-group-item"><span class="glyphicon glyphicon-pushpin">{{customer.education}}</span></li>
            <li class="list-group-item"><span class="glyphicon glyphicon-tag">{{customer.graduationschool}}</span></li>
            <li class="list-group-item"><span class="glyphicon glyphicon-wrench">{{customer.profession}}</span></li>
            <li class="list-group-item"><span class="glyphicon glyphicon-paperclip">{{customer.profile}}</span></li>
        </ul>
    </div>
</template>

<script>
export default {
    name:'customerdetail',
    data(){
        return{
            customer:""
        }
    },
    methods:{
        fetchCustomers(id){
            this.$http.get("http://localhost:3000/users/" + id)
            .then(function(res){
                this.customer = res.body;
                console.log(this.customer);
                
            })
        },
        deleteCustomer(id){
            this.$http.delete("http://localhost:3000/users/"+ id)
                .then(res => {
                    this.$router.push({path:"/",query:{alert:"删除成功"}})
                })
        }
    },
    created(){
        this.fetchCustomers(this.$route.params.id);
    }
}
</script>

<style>

</style>