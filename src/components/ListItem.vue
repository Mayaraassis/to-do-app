<template>
  <li>
    <div class="list-item">
      <input
        type="checkbox"
        :id="index"
        class="item-checkbox"
        @change="$emit('input', $event.target.checked)"
      />
      <label class="item-label" :for="index" :class="getItemClass(item.checked)">{{
        item.label
      }}</label>
    </div>
    <span class="delete" v-html="deleteIcon" @click="deleteItem(index)"></span>
  </li>
</template>

<script>
import feather from "feather-icons";
export default {
  name: "ListItem",
  props: {
    item: Object,
    index: Number,
  },
  computed: {
    deleteIcon() {
      return feather.icons.trash.toSvg({ width: 19 });
    },
  },
  methods: {
    getItemClass(itemChecked) {
      return itemChecked ? 'item-checked': ''
    },

    deleteItem(index) {
      this.$emit("delete-item", index);
    },
  },
};
</script>

<style scoped>
li,
.list-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.item-checked {
  text-decoration: line-through;
}
.item-checkbox {
  margin-right: 10px;
  cursor: pointer;
}
.item-label{
  padding-right: 200px;
  cursor: pointer;
}
.delete{
  cursor: pointer;
}
</style>
