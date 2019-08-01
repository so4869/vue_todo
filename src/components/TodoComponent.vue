<template>
  <div class="todo">
    <div class="row justify-content-center">
      <div class="col-6">
        <h2>Todo List</h2>
      </div>
    </div>

    <div class="row">
      <div class="col">
        <div class="input-group mb-3">
          <input type="text" class="form-control" placeholder="할일 입력">
          <div class="input-group-append">
            <button class="btn btn-outline-secondary" type="button">추가</button>
          </div>
        </div>
      </div>
    </div>

    <div class="row">
      <div class="col">
        <ul class="list-group">
          <li class="list-group-item" v-for="(item, idx) in list">
            <span class="name">{{ item.name }}</span>
            <span class="badge badge-primary">{{ item.date.toLocaleDateString() }}</span>
            <div class="btn-group float-right">
              <button class="btn btn-outline-danger" v-on:click="del(idx)">삭제</button>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        name: 'todo-compo',
        data () {
            return {
                list: [
                    {id: 1, name: '청소하기', date: new Date('2019-08-01')},
                    {id: 2, name: '코딩하기', date: new Date('2019-08-02')},
                    {id: 3, name: '킹능대회 문제풀기', date: new Date('2019-08-03')},
                    {id: 4, name: '문원이 갈구기', date: new Date('2019-08-04')},
                ],
                id: 4,
            }
        },
        methods: {
            del: function(idx){
                this.list.splice(idx, 1);
            }
        }
    }
</script>

<style>
</style>
