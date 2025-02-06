<template>
  <q-page>
    <div class="q-pa-md">
      <q-input color="purple-12" v-model="text" label="To do task" @keyup.enter="addTask">
        <template v-slot:prepend>
          <q-icon name="event" />
        </template>
      </q-input>
      <br />
      <q-btn color="red" icon-right="send" label="Submit" @click="addTask" />

      <br /><br />

      <div class="row">
        <q-list bordered padding class="rounded-borders col-12">
          <q-item-label header>To do Tasak</q-item-label>

          <q-item clickable v-ripple v-for="(task, index) in task" :key="index">
            <q-item-section avatar top>
              <q-avatar icon="assignment" color="grey" text-color="white" />
            </q-item-section>

            <q-item-section>
              <q-item-label>{{ task }}</q-item-label>
            </q-item-section>

            <q-item-section side @click="moveToDone(index)">
              <q-icon name="check" />
            </q-item-section>
          </q-item>
        </q-list>
      </div>
      <br />
      <div class="row">
        <q-list bordered padding class="rounded-borders col-12">
          <q-item-label header>Done Task</q-item-label>

          <q-item clickable v-ripple v-for="(task, index) in done" :key="index">
            <q-item-section avatar top>
              <q-avatar icon="assignment" color="grey" text-color="white" />
            </q-item-section>

            <q-item-section>
              <q-item-label>{{ task }}</q-item-label>
            </q-item-section>

            <q-item-section side @click="deleteTask(index)">
              <q-icon name="close" color="red" />
            </q-item-section>
          </q-item>
        </q-list>
      </div>
    </div>
  </q-page>
</template>
<script>
export default {
  name: 'HomePage1',
  data() {
    return {
      task: [],
      done: [],
      text: '',
    }
  },
  methods: {
    addTask() {
      this.task.push(this.text)
      this.text = ''
    },
    moveToDone(index) {
      this.done.push(this.task[index])
      this.task.splice(index, 1)
    },
    deleteTask(index) {
      this.$q
        .dialog({
          title: 'Confirm',
          message: 'Would you like to Delete This Task?',
          cancel: true,
          persistent: true,
        })
        .onOk(() => {
          this.done.splice(index, 1)
        })
        .onOk(() => {
          // console.log('>>>> second OK catcher')
        })
        .onCancel(() => {
          // console.log('>>>> Cancel')
        })
        .onDismiss(() => {
          // console.log('I am triggered on both OK and Cancel')
        })
    },
  },
}
</script>
<style></style>
