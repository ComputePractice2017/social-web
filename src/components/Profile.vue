<template>
<div class="container">
    <div class="fb-profile">
        <img align="left" class="fb-image-lg" src="http://lorempixel.com/850/280/nightlife/5/" alt="Profile image example">
        <img align="left" class="fb-image-profile thumbnail" src="http://lorempixel.com/180/180/people/9/" alt="Profile image example">
        <div class="fb-profile-text">
            <h1 id="blok1">First Name</h1>
            <h1 id="blok2">Last Name</h1>
            <h3 id="blok3">Years</h3>
            <h3 id="blok4">City</h3>
            <h3 id="blok5">Друзья</h3>
        </div>
    </div>
    <div class="friends">
    <div class="container">
        <form class="form">
                <input  class="form-control" type="text" placeholder="Поиск" id="example-text-input" v-model="search">
            </form>
      <form id="form-inline"class="form-inline">
        <label class="sr-only" for="inlineFormInput">Имя</label>
        <input type="text" v-model.trim="newfriend.FirstName" class="form-control mb-2 mr-sm-2 mb-sm-0"  id="inlineFormInput" placeholder="Имя">
  
        <label class="sr-only" for="inlineFormInputGroup">Фамилия</label>
        <div class="input-group mb-2 mr-sm-2 mb-sm-0">
          
          <input type="text" v-model.trim="newfriend.LastName" class="form-control" id="inlineFormInputGroup" placeholder="Фамилия">
        </div>
  
        <button v-on:click="addnewfriends" v-if="!edit" class="btn btn-primary">Добавить</button>
          <button v-on:click="endedit" v-if="edit" class="btn btn-warning">Сохранить</button>
      </form>
 
      <table  id="table" class="table table-bordered">
          <thead>
          <th>Имя</th>
            <th>Фамилия</th>
        </thead>
        <tbody>
          <tr v-for="friendd in contactList">
            <td>{{friendd.FirstName}}</td>
            <td >{{friendd.LastName}}</td>
            <td>
            <button v-on:click="editfriends(friendd)" v-if="!edit" class="btn btn-warning">Изменить</button>
            <button v-on:click="deletefriends(friendd)" v-if="!edit" class="btn btn-danger">удалить</button>
            </td>
          </tr>
        </tbody>
        </table>
</div> 
    </div>
</div>


</template>

<script>
export default {
  name: 'friends',
  data () {
    return {
      friends: [],
      edit: false,
      newfriend: {
        'FirstName': '',
        'LastName': ''
      },
      search: ''
    }
  },
  computed: {
    contactList: function () {
      var search = this.search
      var filterFn = function (item) {
        return item.FirstName.includes(search) || item.LastName.includes(search)
      }
      if (this.search !== '') {
        return this.friends.filter(filterFn)
      }
      return this.friends
    }
  },
  methods: {
    addnewfriends: function () {
      var obj = {
        'FirstName': '',
        'LastName': ''
      }
      obj.FirstName = this.newfriend.FirstName
      obj.LastName = this.newfriend.LastName
      this.friends.push(obj)
    },
    editfriends: function (obj) {
      this.edit = true
      this.newfriend = obj
    },
    endedit: function () {
      this.edit = false
      var obj = {
        'FirstName': '',
        'LastName': ''
      }
      this.newfriends = obj
    },
    deletefriends: function (obj) {
      var eq = function (input) {
        return input.FirstName === obj.FirstName && input.LastName === obj.LastName
      }
      var index = this.friends.findIndex(eq)
      if (index > -1) {
        this.friends.splice(index, 1)
      }
    }
  }
}

</script>
<style>

#blok1 {
 position:relative;
right:330px;
top: -110px;
}
#blok2 {
 position:relative;
right:-30px;
top: -160px;
}
#blok3 {
 position:relative;
right:245px;
top: -160px;
}
#blok4 {
 position:relative;
right:255px;
top: -165px;
}
#blok5 {
 position:relative;
right:390px;
top: -165px;
}
#table{
     position:relative;
right:0px;
top: -165px;
}
#form-inline{
     position:relative;
right:0px;
top: -190px;
}
#example-text-input{
position:relative;
right:0px;
top: -110px;
}
#table{
  position:relative;
right:0px;
top: -140px;  
}

 body
{
    font-family: 'Open Sans', sans-serif;
}

.fb-profile img.fb-image-lg{
    z-index: 0;
    width: 100%;  
    margin-bottom: 110px;
}

.fb-image-profile
{
    margin: -220px 20px 0px 50px;
    z-index: 9;
    width: 20%; 
}

@media (max-width:768px)
{
    
.fb-profile-text>h1{
    font-weight: 700;
    font-size:16px;
}

.fb-image-profile
{
    margin: -45px 10px 0px 25px;
    z-index: 9;
    width: 20%; 
}
}

</style>
