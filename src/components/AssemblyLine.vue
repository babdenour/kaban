<script setup>
import { reactive, defineProps } from 'vue'

const props = defineProps({
  stages: [String],
})

const itemValues = reactive([])
let inputValue = 'try me'
const clearInput = () => {
  inputValue = ''
}
const changeValue = (event) => {
  if (event.length == 0) {
    return;
  }
  itemValues.push({name: event, status: props.stages[0]})
};

const handleLeftClick = (item, i) => {
  item.status === props.stages[0] ? itemValues.splice(i, 1) : 
  item.status === props.stages[3] ? itemValues[i].status = props.stages[2] : 
  item.status === props.stages[2] ? itemValues[i].status = props.stages[1] :
  item.status === props.stages[1] ? itemValues[i].status = props.stages[0] : "nothing more" 
}
const handleRightClick = (item, i) => {
  item.status === props.stages[3] ? itemValues.splice(i, 1) : 
  item.status === props.stages[0] ? itemValues[i].status = props.stages[1] : 
  item.status === props.stages[1] ? itemValues[i].status = props.stages[2] :
  item.status === props.stages[2] ? itemValues[i].status = props.stages[3] : "nothing more" 
}
</script>

<template>
  <div>
    <label for="item">add an item </label>
    <input data-testid="assembly-add-item" type="text" @change="changeValue($event.target.value)" v-model="inputValue" @keydown.enter="clearInput()" placeholder="try me"/>
  </div>
  <hr />
   <div class="list">
    <div v-for="stage in stages" :key="stageKey"  data-testid="assembly-stage">
      <h3>{{stage}}</h3>
      <div v-for="(itemValue, i) in itemValues" :key="i">
        <p v-if="itemValue.status === stage" @click="handleLeftClick(itemValue, i)"  @contextmenu.prevent="handleRightClick(itemValue, i)" data-testid="assembly-item">{{ itemValue.name }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.list {
  display: flex;
}

.list > div {
  text-align: left;
  margin: 0 30px;
}

p { 
  height: 20px;
  text-align: center;
  border: black 1px solid;
  box-shadow: 2px 1px 0 0;
  cursor: pointer;
}

p:hover {
  background: yellow;
}
</style>
