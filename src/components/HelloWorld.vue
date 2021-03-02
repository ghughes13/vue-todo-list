<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <ol>
      <li v-for="(item, index) in todoItems" :key="item">
        {{ item }} 
        <div>
          <input type="text" class="edit-text" :class="'edit-text-' + [[ index ]]" v-model="editText"/>
          <button v-on:click="showEditApplyBtn(item, index)" class="edit-btn" :class="'edit-for-' + [[ index ]]">Edit</button>
          <button v-on:click="editItem(item, index)" class="apply-edit-btn" :class="'apply-edit-for-' + [[ index ]]">Apply</button>
          <button v-on:click="deleteItem(item)">X</button>
        </div>
      </li>
    </ol>
    <p class="edit-error" v-if="showError">Error: Edited Item Can Not Be Blank</p>
    <input v-model="addItemInput" placeholder="Add Item"/>
    <button type="submit" v-on:click="addItem()">Add</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      todoItems: ['this', 'that', 'other'],
      addItemInput: '',
      editText: '',
      showError: false
    }
  },
  props: {
    msg: String
  },
  methods: {
    addItem () {
      this.todoItems.push(this.addItemInput);
      this.addItemInput = '';
    },
    showEditApplyBtn (item, index) {
      document.querySelectorAll('.edit-btn').forEach(btn => {
        btn.style.display = "inline-block"
      })
      document.querySelectorAll('.apply-edit-btn').forEach(btn => {
        btn.style.display = "none"
      })
      document.querySelectorAll('.edit-text').forEach(btn => {
        btn.style.display = "none"
      })
      document.querySelector('.edit-for-' + index).style.display = "none";
      document.querySelector('.apply-edit-for-' + index).style.display = "inline-block";
      document.querySelector('.edit-text-' + index).style.display = "inline-block";
    },
    editItem (itemToEdit) {
      let foundIndex = this.todoItems.findIndex(toDoItem => toDoItem == itemToEdit );
      if(this.editText === '') {
        this.showError = true
      } else {
        this.todoItems[foundIndex] = this.editText
        this.editText = ''
        this.showError = false
      }
      
    },
    deleteItem (itemToDelete) {
      let foundIndex = this.todoItems.findIndex(toDoItem => toDoItem == itemToDelete );
      if (foundIndex > -1) {
        this.todoItems.splice(foundIndex, 1);
      }
    }
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  text-align: left;
  margin: auto;
  max-width: 400px;
  display: flex;
  justify-content: space-between;
}
a {
  color: #42b983;
}

.edit-text,
.apply-edit-btn {
  display: none;
}
</style>
