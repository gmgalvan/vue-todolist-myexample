<template>
    <div class="list-container">
        <h3>{{ TodoListData.title }}</h3>
       <!-- TODO
        <div class="control__box">
            <div class="control__box__all"><label><input type="checkbox" id="all"> All</label><br></div>
            <div class="control__box__Add">Add <i class="fa fa-plus"></i></div>
        </div>
        -->
        <ul class="list__items">
                <li class="item" v-for="(item, idx) in dataList" :key="item">
                    <input type="checkbox" :id=idx :value=idx  v-model="checked">  {{ item }} 
                    <i @click="deleteItem(item)" :ref="`${idx}_edit`" class="inactive__edit fa fa-trash-o"></i>
                    <i @click="edit(item)" :ref="`${idx}_delete`" class="inactive__delete fa fa-edit"></i> 
                </li>
        </ul>
    </div>
</template>
<script>
export default {
  name: 'TodoList',
  components: {}, 
  props: {
    TodoListData: {
        Type: Object,
    },
  },
  data(){
      return {
        checked: [],
        dataList: [],
      };
  },
  mounted(){
      this.dataList = this.listData;
  },
  methods: {
    edit: function(){
        // TODO
    },
    deleteItem: function(e){
        const idx = this.dataList.indexOf(e)
        this.checked = this.checked.filter((i)=>{
            return idx !== i
        }); 
        this.dataList = this.dataList.filter((el)=>{
            return e !== el;
        }); 
    },
  },
  computed: {
    listData: function () {
      return [...this.TodoListData.listElements];
    }
  },
  watch:{
      checked: function(){
          this.dataList.forEach((e, idx) => {
              if (this.checked.includes(idx)){
                this.$refs[`${idx}_edit`][0].classList.add('active__edit');
                this.$refs[`${idx}_delete`][0].classList.add('active__edit');
                this.$refs[`${idx}_edit`][0].classList.remove('inactive__edit');
                this.$refs[`${idx}_delete`][0].classList.remove('inactive__edit');
              }else{
                this.$refs[`${idx}_edit`][0].classList.remove('active__edit');
                this.$refs[`${idx}_delete`][0].classList.remove('active__edit');
                this.$refs[`${idx}_edit`][0].classList.add('inactive__edit');
                this.$refs[`${idx}_delete`][0].classList.add('inactive__edit');
              }
          }
          );
      },
  },
}
</script>
<style lang="css" scoped>
.list-container{
    width: 600px;
    height: 900px;
    border: 1px solid black;
    display: inline-block;
    border-radius: 100px;
}

.control__box{
    margin: 0 auto;
}
.control__box__all {
    float: left;
    padding-left:20%;
}
.control__box__Add {
    float: left;
    padding-top: 2px;
    padding-left:10%;
}
.list__items {
    padding-top: 20px;
    list-style-type: none;
    clear: both;
    
}
.item {
    border: 1px solid black;
    padding-top: 5%;
    padding-bottom: 5%;
    margin-left: 10%;
    margin-right: 10%;
    margin-top: 1%;
    left: 0;
    padding-left: 0;
    margin-left: 0;
    text-align: justify;
    text-justify: inter-word;
}
.item input{
    margin-left: 10%;
}

.inactive__edit {
    cursor: pointer;
    float: right;
    padding-right: 3%;
    visibility: hidden;
}
.inactive__delete {
    cursor: pointer;
    float: right;
    padding-right: 3%;
    visibility: hidden;
}
.active__edit {
    cursor: pointer;
    float: right;
    padding-right: 3%;
    visibility: visible;
}
.active__delete {
    cursor: pointer;
    float: right;
    padding-right: 3%;
    visibility: visible;
}

</style>