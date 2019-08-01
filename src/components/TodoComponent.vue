<template>
  <div class="todo">
    <div class="row justify-content-center">
      <div class="col-6">
        <h2>Todo List</h2>
      </div>
      <div class="col-6"></div>
    </div>

    <div class="row">
      <div class="col">
        <div class="input-group mb-3">
          <input type="text" class="form-control" placeholder="할일 입력" v-model="todoText">
          <div class="input-group-append">
            <button class="btn btn-outline-secondary" type="button" v-on:click="add">추가</button>
          </div>
        </div>
      </div>
    </div>

    <div class="row">
      <div class="col">
        <transition-group tag="ul" name="gondr" class="list-group">
          <li class="list-group-item" v-for="(item, idx) in list" :key="item.id">
            <span class="name">{{ item.name }}</span>
            <span class="badge badge-primary">{{ item.date.toLocaleDateString('ko') }}</span>
            <div class="btn-group float-right">
              <button class="btn btn-outline-success" v-on:click="complete(idx)">완료</button>
              <button class="btn btn-outline-danger" v-on:click="del(idx)">삭제</button>
            </div>
          </li>
        </transition-group>
      </div>
    </div>


    <div class="row justify-content-center">
      <div class="col-6">
        <h2>Complete List</h2>
      </div>
      <div class="col-6"></div>
    </div>
    <div class="row">
      <div class="col">
        <transition-group tag="ul" name="gondr" class="list-group">
          <li class="list-group-item" v-for="(item, idx) in cList" :key="item.id">
            <span class="name">{{ item.name }}</span>
            <span class="badge badge-success">{{ item.date.toLocaleDateString('ko') }}</span>
          </li>
        </transition-group>
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        name: 'todo-compo',
        mounted () {
            this.$http.get('http://localhost/read.php')
                .then( res => {
                    let temp = res.data.map( x => {
                        x.date = new Date(x.date);
                        return x;
                    });
                    this.list = temp;
                    this.id = temp.length;
                } );

        },
        data () {
            return {
                list: [],
                id: 4,
                todoText: '',
                cList: [],
            }
        },
        methods: {
            del: function(idx){
                this.list.splice(idx, 1);
            },
            add: function(){
                if(this.todoText.trim() === '') return alert('공백');

                let temp = {id: ++this.id, name: this.todoText, date: new Date()};
                this.list.push(temp);

                this.todoText = '';


                let form = new FormData();
                form.append('name', this.todoText);
                this.$http.post('http://localhost/post.php', form)
                    .then( res => console.log(res.data) );
            },
            complete: function(idx){
                let temp = this.list.splice(idx, 1)[0];
                temp.date = new Date();
                this.cList.push(temp);
            }
        }
    }
</script>

<style scoped>
  .gondr-enter-active, .gondr-leave-active{
    transition: 0.7s;
  }
  .gondr-enter, .gondr-leave-to{
    transform: translateX(-100px);
    opacity: 0;
  }
</style>
