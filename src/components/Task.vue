<template>
  <li class="todo__item">
    <p 
        class="todo__description" 
        :class="['todo__description', {'todo__description--active': isComplete}]"
    >{{text}}</p>
    <input class="todo__status" type="checkbox" v-model="isComplete" />
  </li>
</template>

<script>
export default {
    name: "task",
    props: {
        text: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            isComplete: false,
        }
    }
};
</script>

<style lang="scss">
.todo {
  &__item {
    display: grid;
    grid-template-columns: 1fr 40px;
    background: #fff;
  }

  &__item + &__item {
    margin-top: 15px;
  }

  &__description {
    padding: 10px 10px;
    margin: 0;
    word-break: break-all;

    &--active {
      text-decoration: line-through;
      opacity: 0.3;
    }
  }

  &__status {
    justify-self: center;
    margin-top: 12px;
    width: 20px;
    height: 20px;
  }
}
</style>