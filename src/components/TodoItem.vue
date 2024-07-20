<template>
  <div>
    <!-- Contenedor principal de la columna -->
    <el-col :span="12">
      <!-- Tarjeta para mostrar el contenido de la tarea o item -->
      <el-card class="box-card" shadow="hover" style="margin: 5px 0;">
        <el-row :gutter="12">
          <!-- Columna para mostrar el título de la tarea o item -->
          <el-col :span="21">{{ todo }}</el-col>
          <!-- Columna para el botón de eliminar/cerrar -->
          <el-col :span="3">
            <el-button @click="removeTodo" type="success" icon="el-icon-check" circle></el-button>
          </el-col>
        </el-row>
      </el-card>
    </el-col>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: String,
    index: Number,
  },
  methods: {
    removeTodo() {
      this.$emit('remove-todo', this.index);
    }
  }
}



/*export default {
  name: 'TodoItem',
  props: {
    // Propiedad para el texto de la tarea
    todo: {
      type: String,
      required: true
    },
    // Propiedad para el objeto del issue
    issue: {
      type: Object,
      required: false
    },
    // Propiedad para el índice del elemento
    index: {
      type: Number,
      required: true
    },
  },
  methods: {
    removeItem() {
      // Emitir evento adecuado según el tipo de elemento
      if (this.type === 'todo') {
        // Emitir evento para eliminar tarea
        this.$emit('remove-todo', this.index);
      } else if (this.type === 'issue') {
        // Emitir evento para cerrar issue
        this.$emit('close-issue', this.index);
      }
    }
  }
}*/
</script>


  