<template>
  <draggable class="list" :list="listData">
    <ListItem
      v-for="item in listData"
      :key="item.id"
      v-bind="{
        icon: item.icon,
        checked: item.checked,
        data: item.data,
        number: item.number,
        click: (e) => onItemClick(e),
      }"
      @onChipClick="onChipClick"
      @onClickItem="onItemClick"
      @onClickCheckbox="(value) => onClickCheckbox({ value, id: item.id })"
    />
  </draggable>
</template>
<script>
import draggable from "vuedraggable";
import ListItem from "./ListItem.vue";
export default {
  name: "List",
  components: { ListItem, draggable },
  data() {
    return {
      listData: [
        { id: 1, data: "data1", checked: true, type: "checkbox" },
        { id: 2, data: "data1", checked: null, type: "input" },
        { id: 3, data: "data3", checked: null, type: "text" },
      ],
    };
  },
  methods: {
    onChipClick() {},
    onItemClick(e) {
      console.log(e);
    },
    onClickCheckbox(args) {
      console.log(args);
      const { value, id } = args;
      this.listData.forEach((item) => {
        if (item.id == id) {
          item.checked = value;
        }
      });
    },
  },
};
</script>
<style lang="scss" scoped>
.list {
  display: flex;
  gap: 15px;
}
</style>
