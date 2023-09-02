<!-- LAYOUT example: https://thecodeplayer.com/experiments/css3-family-tree-multiple-parents.html# -->
<script setup lang="ts">
import { ref, onMounted } from 'vue'
const props = defineProps(['familyTree'])
// const props = defineProps({
//     familyTree: Object,
//     familyData: Object,
//     familyMembers: Object,
//     sortedFamilyMembers: Object
// })
// defineProps({
//   familyTree: Object,
//   familyData: Object,
//   familyMembers: Object,
//   sortedFamilyMembers: Object
// })
// export interface Props {
//   familyTree: Object,
//   familyData: Object,
//   familyMembers: Object,
//   sortedFamilyMembers: Object
// }
// withDefaults(defineProps<{
//     familyTree: Object,
//     // familyData: Object,
//     // familyMembers: Object,
//     // sortedFamilyMembers: Object
// }>(), {
//   familyMembers = familyTree
// })

// let self = this
// const familyData = props.familyTree
// console.log('familyData', familyData)
// let familyMembers = familyData.family.members
// let sortedFamilyMembers:Object = familyMembers.sort((a:any,b:any) => {
//   return a.generation - b.generation
// })

// console.log('familyMembers:', familyMembers)
// console.log('sortedFamilyMembers:', sortedFamilyMembers)

const familyData = props.familyTree
console.log('familyData', familyData)
let familyMembers = familyData.family.members
familyMembers.sort((a: { generation: number; },b: { generation: number; }) => {
  return a.generation - b.generation
})

// TODO: figure out a way to display each generation without skipping or duplicating anyone. AND display the partners together!
// for(const value of familyMembers) {
//   console.log(value)
// }

console.log('members:', familyMembers)
onMounted(() => {
  //let self = this
  //const familyData = props.familyTree
  console.log('onMounted')
})

</script>
<template>
    <div>
      <!-- Generation -->
      <ul v-if="familyData" class="generation">
        <!-- make a for loop based on generation. Once the generation is all populated, move on to next generation number. Perhaps let this template call itself? -->
          <li>
              <a href="#">Parent</a>
              <ul>
                  <li>
                      <a href="#">Child</a>
                  </li>
                  <li>
                      <a href="#">SubParent 1</a>
                      <a href="#">SubParent 2</a>
                      <ul>
                          <li><a href="#">Grandchild</a></li>
                          <li><a href="#">Grandchild</a></li>
                          <li><a href="#">Grandchild</a></li>
                      </ul>
                  </li>
              </ul>
          </li>
      </ul>
      <div class="item">
        <i>
          <slot name="icon"></slot>
        </i>
        <div class="details">
          <h3>
            <slot name="heading"></slot>
          </h3>
          <slot></slot>
        </div>
      </div>
    </div>
  </template>
  <style scoped>
  .item {
    margin-top: 2rem;
    display: flex;
    position: relative;
  }
  
  .details {
    flex: 1;
    margin-left: 1rem;
  }
  
  i {
    display: flex;
    place-items: center;
    place-content: center;
    width: 32px;
    height: 32px;
  
    color: var(--color-text);
  }
  
  h3 {
    font-size: 1.2rem;
    font-weight: 500;
    margin-bottom: 0.4rem;
    color: var(--color-heading);
  }
  
  @media (min-width: 1024px) {
    .item {
      margin-top: 0;
      padding: 0.4rem 0 1rem calc(var(--section-gap) / 2);
    }
  
    i {
      top: calc(50% - 25px);
      left: -26px;
      position: absolute;
      border: 1px solid var(--color-border);
      background: var(--color-background);
      border-radius: 8px;
      width: 50px;
      height: 50px;
    }
  
    .item:before {
      content: ' ';
      border-left: 1px solid var(--color-border);
      position: absolute;
      left: 0;
      bottom: calc(50% + 25px);
      height: calc(50% - 25px);
    }
  
    .item:after {
      content: ' ';
      border-left: 1px solid var(--color-border);
      position: absolute;
      left: 0;
      top: calc(50% + 25px);
      height: calc(50% - 25px);
    }
  
    .item:first-of-type:before {
      display: none;
    }
  
    .item:last-of-type:after {
      display: none;
    }
  }
  </style>
  