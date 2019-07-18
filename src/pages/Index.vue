<template>
  <q-page padding>
    <div class="row q-mb-lg">
      <q-input v-model="newTask" label="Add new task" class="col" @keyup.enter="addTask" />
      <q-btn color="primary" label="Add" @click.native="addTask" />
    </div>
    <div class="row q-mb-lg">
      <q-list bordered separator class="col">
        <q-list-header>Tasks</q-list-header>
        <q-item clickable v-ripple v-for="(task, index) in tasks" v-bind:key="task">
          <q-item-section>{{task}}</q-item-section>
          <q-btn outline style="color: goldenrod;" label="Done" @click.native="moveToDone(index)" />
        </q-item>
      </q-list>
    </div>

    <div class="row q-mb-lg">
      <q-list bordered separator class="col">
        <q-list-header>Done</q-list-header>
        <q-item clickable v-ripple v-for="(task, index) in done" v-bind:key="task">
          <q-item-section>{{task}}</q-item-section>
          <q-btn label="Excluir" color="primary" @click.native="deleteTask(index)" />
        </q-item>
      </q-list>
    </div>
  </q-page>
</template>
<style>
</style>

<script>

export default {
  name: 'PageIndex',
  data () {
    return {
      tasks: [],
      done: [],
      newTask: ''
    }
  },
  methods: {
    addTask () {
      this.tasks.push(this.newTask)
      this.newTask = ''
    },
    moveToDone (index) {
      this.done.push(this.tasks[index])
      this.tasks.splice(index, 1)
    },
    deleteTask (index) {
      this.$q
        .dialog({
          title: 'Confirmar',
          message: 'Gostaria de excluir a tarefa?',
          cancel: true,
          persistent: true
        })
        .onOk(() => {
          console.log('>>>> OK')
        })
        .onOk(() => {
          this.done.splice(index, 1)
          console.log('>>>> second OK catcher')
        })
        .onCancel(() => {
          console.log('>>>> Cancel')
        })
        .onDismiss(() => {
          console.log('I am triggered on both OK and Cancel')
        })
    }
  }
}
</script>
