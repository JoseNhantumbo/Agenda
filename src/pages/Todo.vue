<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
        v-model="newTask"
        @keyup.enter="addTask"
        class="col"
        square
        filled
        bg-color="white"
        placeholder="Adicionar uma tarefa"
        dense>
        <template v-slot:append>
          <q-btn
            @click="addTask"
            round
            dense
            flat
            icon="add" />
        </template>
      </q-input>
    </div>
    <q-list
      class="bg-white"
      separator
      bordered>
      <q-item
        v-for ="(task,index) in tasks"
        :key ="task.title"
        @click="task.done = !task.done"
        :class = "{'done bg-blue-2' : task.done}"
        clickable
        v-ripple>
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            class ="no-pointer-events"
            color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.title}}</q-item-label>
        </q-item-section>
        <q-item-section
          v-if="task.done"
          side>
          <q-btn
            @click.stop="deleteTask(index)"
            flat
            round
            dense
            color="red"
            icon="delete" />
        </q-item-section>
      </q-item>
    </q-list>
    <div
      v-if="!tasks.length"
      class="no-tasks absolute-center">
      <q-icon
        name="check"
        size="100px"
        color="primary"
      />
      <div class="text-h6 text-primary text-center">
        Sem Tarefas
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      newTask :'',
      tasks : [
        /*{
        title: 'Comprar um BMW',
        done : false
      },
        {
          title: 'Comprar um Avião',
          done : true
        },
        {
          title: 'Comprar um Navio',
          done : false
        }*/
      ]
    }
  },
  methods :{
    deleteTask(index) {
        this.$q.dialog({
          dark: true,
          title: 'Confirmação',
          message: 'Deseja remover a tarefa??',
          cancel: true,
          persistent: true
        }).onOk(() => {
          this.tasks.splice(index, 1)
          this.$q.notify('Tarefa removida com sucesso')
        })

    },
    addTask() {
      this.tasks.push({
        title: this.newTask,
        done: false
      })
      this.newTask=''
    }
  }
}
</script>

<style lang="scss">
   .done{
     .q-item__label {
       text-decoration:  line-through;
       color : #bbb;
     }
   }
  .no-tasks {
    opacity: 0.5;
  }
</style>
