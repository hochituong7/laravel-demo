<template>
  <div class="hello">
    <div class="container">
      <div class="card">
        <div class="card-body">
          <div class="input-group mb-3">
            <input type="text" class="form-control"
                    v-model="inputName"
                    placeholder="Enter name..." 
                    aria-label="Recipient's username" 
                    aria-describedby="button-addon2"/>
            <button 
              class="btn btn-outline-secondary" 
              type="button" 
              id="button-addon2" 
              v-on:click="AddNew"
            >Add</button>
          </div>
          <hr/>
          <ul class="list-group list-group-flush list-item">
            <li v-if="list.length === 0">Empty item</li>
            <li class="list-group-item" 
              v-for="(item,index) in list" :key="item.id">
              <span class="item-content">{{item.name}}</span>
              <span class="item-action">
                <button type="button" class="btn btn-success btn-sm action-btn" v-on:click="UpItem(index)" :disabled="index ===0 ? '' : disabled">Up</button>
                <button type="button" class="btn btn-success btn-sm action-btn" v-on:click="DownItem(index)" :disabled="index === list.length - 1 ? '' : disabled">Down</button>
                <button type="button" class="btn btn-danger btn-sm action-btn" v-on:click="DeleteItem(item)">Delete</button>
              </span>
            </li>
          </ul>
         
        </div>
      </div>    
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods:{ 
    AddNew(){ 
       if( this.inputName === ""){
        alert('Dữ liệu không được rỗng !');
        return;
       }
        this.list.push({name: this.inputName});
        this.inputName = "";
    }
    ,
    DeleteItem(item){
      this.list = this.list.filter((t) => t !== item)
    },
    UpItem(index){
      var valueCurrent = this.list[index];
      var valueNext =  this.list[index-1];
      this.list[index] = valueNext;
      this.list[index-1] = valueCurrent;
    },
    DownItem(index){
      var valueCurrent = this.list[index];
      var valueNext =  this.list[index+1];
      this.list[index] = valueNext;
      this.list[index+1] = valueCurrent;
    }
  },
  data(){
    return {
      inputName: "",
      list:[
        // {
        //   name:"Hồ Chí Tưởng"
        // },
        // {
        //   name:"Nguyễn Văn A"
        // },
        // {
        //   name:"Nguyễn Văn B"
        // },
        // {
        //   name:"Nguyễn Văn C"
        // },
        // {
        //   name:"Nguyễn Văn D"
        // }
      ]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.card{
  width: 800px;
  margin: 0 auto;
}
.list-item{
  text-align: left;
}
.item-action{
  float: right;
}
.action-btn{
  margin-left: 3px;
}
</style>
