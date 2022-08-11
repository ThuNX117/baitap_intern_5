<template>
  <div class="item" @click="onItemClick">
    <div class="item--checkbox" v-if="isShowCheckbox">
      <input type="checkbox" class="checkbox" v-model="isCheck" />
    </div>
    <div class="item--context">
      <i class="item--context__icon" :class="icon" v-show="isShowIcon" />
      <span class="item--context__text">{{ data }}</span>
    </div>
    <div class="item--chip" v-if="isShowChip" @click.stop="onChipClick">
      <span class="item--chip__text">{{ number }}</span>
    </div>
  </div>
</template>
<script>
export default {
  name: "ListItem",
  props: {
    icon: { type: String, required: false },
    variant: { type: String, required: false, default: "" },
    checked: { type: Boolean, required: false, default: false },
    data: {
      type: [String, Number],
      required: true,
      validator: function (value) {
        if (value && String(value).length > 0) {
          return true;
        }
        return false;
      },
    },
    number: {
      type: Number,
      required: false,
    },
    click: {
      type: Function,
    },
  },
  watch: {
    isCheck() {
      this.$emit("onClickCheckbox", this.isCheck);
    },
  },
  created() {
    this.isCheck = this.checked;
  },
  data() {
    return { isCheck: false };
  },
  computed: {
    isShowChip() {
      return Boolean(this.number);
    },
    isShowIcon() {
      return !!this.icon;
    },
    isShowCheckbox() {
      return this.checked != null;
    },
  },
  methods: {
    onClickCheckbox($event) {
      console.log($event);
      // const value = $event.target.checked;
      this.$emit("onClickCheckbox", this.checked);
    },
    onItemClick() {
      console.log("clickItem");
    },
  },
};
</script>
<style lang="scss" scoped>
.item {
  display: flex;
  padding: 10px;
  border: 1px solid #dcdcdc;
  border-radius: 4px;
  align-items: center;
  justify-content: flex-start;
  gap: 8px;
}
</style>
