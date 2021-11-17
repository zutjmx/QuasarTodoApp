<template>
  <q-page class="bg-gray-3 column">
    <q-list class="bg-white"
            separator
            bordered
    >
      
      <q-item v-for="(task, index) in tasks"
              :key="task.title"
              @click="task.done = !task.done"
              :class="{'done bg-blue-1': task.done}"
              clickable
              v-ripple
      >
        <q-item-section avatar>
          <q-checkbox v-model="task.done" 
                      class="no-pointer-events"
                      color="primary" 
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>
            {{task.title}}
          </q-item-label>
        </q-item-section>
        <q-item-section
          v-if="task.done"
          side
        >
          <q-btn 
              @click.stop="deleteTask(index)"
              flat 
              round 
              color="primary" 
              icon="delete"
              dense 
          />
        </q-item-section>
      </q-item>

    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  data() {
    return {
      tasks: [
        {
          title: 'Mole',
          done: false
        },
        {
          title: 'Pollo',
          done: false
        },
        {
          title: 'Arroz',
          done: false
        },
        {
          title: 'Frijoles',
          done: false
        },
      ]
    }
  },
  methods: {
    deleteTask(index) {

      this.$q.dialog({
        title: 'Confirmación',
        message: '¿Desea borrar la tarea?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index,1)
        this.$q.notify({
          message: 'La tarea se borró.',
          color: 'red',
          icon: 'folder_delete'
        })
      }).onCancel(() => {
        this.$q.notify({
          message: 'La tarea no se borró.',
          color: 'green',
          icon: 'health_and_safety'
        })
      })
      
    }
  }
})
</script>

<style lang="scss">
  .done {
    .q-item__label {
      text-decoration: line-through;
      color: #bbb;
    }
  }
</style>