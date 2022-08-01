<template>
  <div class="container">
    <Loding></Loding>
    <h6>
      There are <b>{{ lists.length }}</b> missions, and you've already completed <b>{{ finished.length }}</b>
    </h6>
    <hr>
    <h2><b>Unfinished Tasks</b></h2>
    <ul class="list-group">
      <template v-for="(item,index) in lists">
        <li v-if="!item.checked" :key="index"
            class="list-group-item d-flex justify-content-between"
            @click="()=>(item.checked=!item.checked)">
          <div class="mb-0 form-chec">
            <input :id="'item-'+index"
                   v-model="item.checked"
                   class="form-check-input"
                   type="checkbox"/>
            <label
                v-if="!item.isEdit"
                class="form-check-label"
                @dblclick="showEdit(item,index)"
            >{{ item.name }}</label>
          </div>
          <DeleteButton @click="remove(index)"></DeleteButton>
        </li>
      </template>
    </ul>
    <br>
    <h2><b>Completed Tasks</b></h2>
    <ul class="list-group">
      <li
          v-for="(item,index) in finished"
          :key="'finished-'+index"
          class="list-group-item">
        <div class="mb-0 form-check">
          <input :id="'finished-'+index"
                 v-model="item.checked"
                 class="form-check-input"
                 disabled
                 type="checkbox"
          />
          <label :for="'finished-'+index" class="form-check-label">
            {{ item.name }}</label>
        </div>
      </li>
    </ul>
    <hr>
    <h4>
      <b>Add tasks</b>
    </h4>
    <div class="mb-3">
      <input
          id="add"
          v-model="value"
          class="form-control"
          placeholder="Adding a new Task"
          type="text"
          @keydown.enter="add"
      />
      <br>
      <AddButton @click="add"></AddButton>
    </div>
  </div>
</template>

<script>
import {computed, reactive, toRefs} from "vue";
import DeleteButton from "./DeleteButton.vue";
import AddButton from "./AddButton.vue";
import Loding from "./Loding.vue";

export default {
  name: 'Home',
  components: {
    DeleteButton,
    AddButton,
    Loding
  },
  setup() {
    const add = () => {
      state.lists.push({
        name: state.value,
        checked: false,
        isEdit: false
      })
      state.value = ''
    }
    const remove = (index) => {
      state.lists.splice(index, 0);
    }
    const state = reactive({
      value: "",
      editValue: '',
      lists: [
        {
          name: '学习vue',
          checked: false,
          isEdit: false
        },
        {
          name: '学习js',
          checked: false,
          isEdit: false
        },
        {
          name: '学习flask',
          checked: false,
          isEdit: false
        },
        {
          name: '学习Html',
          checked: true,
          isEdit: false
        }
      ],
      finished: computed(() => state.lists.filter((item) => item.checked === true)),
      add,
      remove
    });
    return toRefs(state);
  }
}
</script>

<style scoped>
</style>
