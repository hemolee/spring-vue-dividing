<template>
<div>
  <Nav></Nav>
  <form>
    <div class="form-group">
      <label for="email">ID:</label>
      <input type="text" class="form-control" v-model="customerId" id="email" placeholder="Enter email">
    </div>
    <div class="form-group">
      <label for="pwd">Password:</label>
      <input type="text" class="form-control" v-model="password" id="pwd" placeholder="Enter password">
    </div>
    <div class="checkbox">
      <label><input type="checkbox"> Remember me</label>
    </div>
    <button class="btn btn-default" @click="count">count</button>
    <button class="btn btn-default" @click="deleteById">deleteById</button>
    <button class="btn btn-default" @click="existsById">existsById</button>
    <button class="btn btn-default" @click="findAll">findAll</button>
    <button class="btn btn-default" @click="findById">findById</button>
    <button class="btn btn-default" @click="save">save</button>
    <button class="btn btn-default" @click="login">login</button>
  </form>
  <Footer></Footer>
</div>
</template>

<script>
import Nav from '@/components/common/Nav.vue'
import Footer from'@/components/common/Footer.vue'
import axios from 'axios'

export default {
   data(){
    return{
        context : 'http://localhost:9000/customers',
        customerId : 'hong111111',
        customerName : '홍길동',
        password : '1234',
        ssn:'910701-122222',
        phone : '010-1111',
        city : '서울',
        address :'서울시 종로구',
        postalcode :'01752',
        photo :'0000'

    }
  },
  components: {
    Nav,
    Footer
  },
  methods:{     
    count(){
        axios.get(`${this.context}/count`)
         .then(res=>{           
             alert(`count() SUCCESS2 : ${res.data}`)
         })
         .catch(e=>{
             alert('ERROR')
         })
      } ,
      deleteById(){
        axios.delete(`${this.context}/1`)
         .then(res=>{           
             alert(`deleteById() SUCCESS2 : ${res.data}`)
         })
         .catch(e=>{
             alert('ERROR')
         })
      },
      existsById(){
        axios.get(`${this.context}/exists/1`)
         .then(res=>{           
             alert(`existsById SUCCESS2 : ${res.data}`)
         })
         .catch(e=>{
             alert('ERROR')
         })
      },
      findAll(){
        axios.get(`${this.context}`)
         .then(res=>{           
             alert(`findAll : ${res.data[0].customerName}`)
         })
         .catch(e=>{
             alert('ERROR')
         })
      },
      findAllById(){
        axios.get(`${this.context}/1`)
         .then(res=>{           
             alert(`findAllById : ${res.data}`)
         })
         .catch(e=>{
             alert('ERROR')
         })
      },
      findById(){
        axios.get(`${this.context}/1`)
         .then(res=>{           
             alert(`findById : ${res.data.customerName}`)
         })
         .catch(e=>{
             alert('ERROR')
         })
      },
      save(){
        let data = { //dto랑 이름 일치해야 에러안남.
          customerId : this.customerId,
          customerName : this.customerName,
          password :this.password,
          ssn:this.ssn,
          phone : this.phone,
          city : this.city,
          address :this.address,
          postalcode :this.postalcode,
          photo :this.photo
        }
        let headers ={
          'Content-Type': 'application/json',
          'Athorization': 'JWT fefege..'
        }
        axios.post(`${this.context}`,
                   JSON.stringify(data),
                    {headers: headers})
         .then(res=>{           
             alert(`save : ${res.data}`)
         })
         .catch(e=>{
             alert('ERROR')
         })
      },
      login(){                  
        axios.get(`${this.context}/login`)
         .then(res=>{           
             alert(`login : ${res.data.customerId}`)
         })
         .catch(e=>{
             alert('ERROR')
         })  
      }
  }
}
</script>

<style scoped>
</style>