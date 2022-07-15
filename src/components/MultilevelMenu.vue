<template>
  <ul>
    <li
      v-for="dish in filteredDishes"
      :key="dish.name"
      :style="{ 'margin-left': `${depth * 5}px` }"
      class="dish"
    >
      <div class="dish-item__container">
        <span
          class="dish"
          @click="dishClicked(dish)"
          v-if="dish.menuItems && dish.menuItems.length > 0"
          >{{ isExpanded(dish) ? "&#9660;" : "&#9658;" }}</span
        >
        <div class="dish-item" :class="{ top: depth === 1 }">
          {{ dish.name }} <span></span>
          {{ dish.menuItems ? `( ${dish.menuItems.length} )` : "" }}
        </div>
        <img
          src="@/assets/icons/create.svg"
          class="dish-item--icon"
          @click="elementConsistCheck(dish.name)"
        />
        <img
          src="@/assets/icons/delete.svg"
          class="dish-item--icon"
          @click="deleteElement(dish)"
        />
      </div>
      <AddDishInput
        v-if="checkDish(dish.name).includes(dish.name)"
        @detect-input-value="addNewDishItem($event, dish)"
      />
      <MultilevelMenu
        v-if="isExpanded(dish) && dish.menuItems"
        :menu="dish.menuItems"
        :depth="depth + 1"
        @onClick="(dish) => $emit('onClick', dish)"
      />
    </li>
  </ul>
</template>

<script>
import AddDishInput from "@/components/AddDishInput";
export default {
  name: "MultilevelMenu",
  components: {
    AddDishInput,
  },
  props: {
    menu: Array,
    depth: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      expanded: [],
      newMenuValue: "",
      listDishesToAdd: [],
      filteredItems: [],
    };
  },
  methods: {
    isExpanded(dish) {
      return this.expanded.indexOf(dish) !== -1;
    },
    openModal() {
      this.$modal.show("extraDish");
    },
    closeModal() {
      this.$modal.hide("extraDish");
    },
    dishClicked(dish) {
      if (!this.isExpanded(dish)) {
        this.expanded.push(dish);
      } else {
        this.expanded.splice(this.expanded.indexOf(dish));
      }
    },
    elementConsistCheck(dish) {
      this.listDishesToAdd.push(dish);
    },
    checkDish(dish) {
      return this.listDishesToAdd.filter((el) => el === dish);
    },
    deleteElement(dish) {
      if (dish.menuItems && dish.menuItems.length === 0) {
         dish.menuItems = [];
      } else {
        this.filteredItems =
          this.filteredItems.length === 0
            ? this.menu.filter((el) => el.name !== dish.name)
            : this.filteredItems.filter((el) => el.name !== dish.name);
      }
    },
    addNewDishItem(value, dish) {
      dish.menuItems
        ? dish.menuItems.push({ name: value })
        : (dish.menuItems = [{ name: value }]);
      if (!this.isExpanded(dish)) {
        this.expanded.push(dish);
      }
      this.listDishesToAdd = this.listDishesToAdd.filter((el) => el === dish);
      alert( `${dish.name} : ${value}`)
    },
  },
  computed: {
    filteredDishes() {
      return this.filteredItems.length === 0 ? this.menu : this.filteredItems;
    },
  },
};
</script>

<style scoped>
.top {
  color: #66f6ff;
}

.dish {
  text-align: left;
  font-size: 18px;
  margin-right: 10px;
}
.dish-item {
  display: inline-block;
}
ul {
  list-style: none;
}
li {
  margin: 20px auto;
}
.dish-item--icon {
  margin-left: 20px;
}
.dish-item__container {
  margin: 20px;
}
</style>
