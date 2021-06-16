<template>
  <div class="todo" :style="{ background: colors[day] }">
    <div class="todo__wrapper">
      <h1 class="todo__title">{{ title }}</h1>
      <form class="todo__form form">
        <input
          type="text"
          :class="['form__input', `form__input--color${nextDay}`]"
          v-model="task"
        />
        <button
          :class="['form__btn', 'btn', `btn--color${nextDay}`]"
          @click.prevent="addNote"
        >
          add
        </button>
      </form>
      <div class="todo__wrap" v-if="notes.length">
        <ul :class="['todo__list', `todo__list--color${nextDay}`]">
          <task v-for="(note, i) in notes" :key="i" :text="note"></task>
        </ul>
        <div class="todo__button-group">
          <button
            :class="['todo__btn', 'btn', `btn--color${nextDay}`]"
            @click="removeAll"
          >
            Remove All
          </button>
        </div>
      </div>
      <p class="todo__text" v-else>notes is empty</p>
    </div>
  </div>
</template>

<script>
import task from "./components/Task.vue";

export default {
  name: "App",
  components: { task },
  data() {
    return {
      title: "Vue-cli-todo",
      colors: [
        "#C0A000",
        "#167b5b",
        "#1FA08F",
        "#3F70F0",
        "#A00000",
        "#EA8000",
        "#8900F0",
      ],
      day: new Date().getDay(),
      nextDay: this.day !== 6 ? new Date().getDay() + 1 : 0,
      task: "",
      notes: JSON.parse(localStorage.getItem("notes") || "[]"),
    };
  },
  methods: {
    addNote() {
      if (this.task !== "" && !this.notes.includes(this.task.trim())) {
        this.notes.push(this.task.trim());
        localStorage.setItem("notes", JSON.stringify(this.notes));
        this.task = "";
      }
    },
    removeAll() {
      const count = this.notes.length;
      this.notes.splice(0, count);
      localStorage.clear();
    },
  },
};
</script>

<style lang="scss">
$sunday: #c0a000;
$monday: #167b5b;
$tuesday: #1fa08f;
$wednesday: #3f70f0;
$thursday: #a00000;
$friday: #ea8000;
$saturday: #8900f0;

@mixin adaptFont($pcSize, $mobSize, $maxSize) {
  $addSize: $pcSize - $mobSize;
  @if $maxSize==1 {
    font-size: $pcSize + px;

    @media (max-width: #{1170 + px}) {
      font-size: calc(
        #{$mobSize + px} + #{$addSize} * ((100vw - 320px) / #{1170 - 320})
      );
    }
  } @else {
    font-size: calc(
      #{$mobSize + px} + #{$addSize} * ((100vw - 320px) / #{1170 - 320})
    );
  }
}

@mixin btnhov($color) {
  color: #fff;
  border: 2px solid $color;
  background: $color;
  box-shadow: 0 0 10px $color;
}

#app {
  display: grid;
  place-items: center;
  width: 100vw;
  height: 100vh;
  background: #242424;
  font-family: "Open Sans", sans-serif;
  overflow: hidden;
}

.btn {
  display: grid;
  place-items: center;
  color: #fff;
  border: 2px solid #fff;
  border-radius: 5px;
  transition: 0.35s ease;
  cursor: pointer;

  &--color0:hover {
    @include btnhov($sunday);
  }
  &--color1:hover {
    @include btnhov($monday);
  }
  &--color2:hover {
    @include btnhov($tuesday);
  }
  &--color3:hover {
    @include btnhov($wednesday);
  }
  &--color4:hover {
    @include btnhov($thursday);
  }
  &--color5:hover {
    @include btnhov($friday);
  }
  &--color6:hover {
    @include btnhov($saturday);
  }

  &:focus {
    outline: none;
  }
}

.todo {
  display: flex;
  justify-content: center;
  width: 90%;
  border-radius: 15px;

  &__wrapper {
    display: grid;
    place-items: center;
    grid-template-rows: 0.1fr 0.1fr 1fr;
  }

  &__title {
    font-family: "Comfortaa", cursive;
    color: #fff;
  }

  &__form {
    display: grid;
    grid-template-columns: 0.5fr 60px;
    justify-content: center;
    grid-column-gap: 10px;

    width: 100%;

    padding: 20px 0;
  }

  &__wrap {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;
    width: 100%;
  }

  &__list {
    padding: 0 5px 0 0;
    overflow: auto;

    &::-webkit-scrollbar {
      width: 5px;
    }

    &::-webkit-scrollbar-thumb {
      border-radius: 15px;
    }

    &--color0::-webkit-scrollbar-thumb {
      background: $sunday;
    }
    &--color1::-webkit-scrollbar-thumb {
      background: $monday;
    }
    &--color2::-webkit-scrollbar-thumb {
      background: $tuesday;
    }
    &--color3::-webkit-scrollbar-thumb {
      background: $wednesday;
    }
    &--color4::-webkit-scrollbar-thumb {
      background: $thursday;
    }
    &--color5::-webkit-scrollbar-thumb {
      background: $friday;
    }
    &--color6::-webkit-scrollbar-thumb {
      background: $saturday;
    }
  }

  &__button-group {
    display: grid;
    justify-content: center;
    width: 100%;
    padding-bottom: 10px;
  }

  &__btn {
    padding: 0.5em 1em;
  }

  &__text {
    @include adaptFont(48, 30, 1);
    color: #fff;
    text-transform: uppercase;
  }
}

.form {
  &__input {
    border: none;
    border-bottom: 2px solid #fff;
    color: #fff;
    transition: 0.3s ease;

    &:focus {
      outline: none;
    }

    &--color0:focus {
      border-bottom: 2px solid $sunday;
    }
    &--color1:focus {
      border-bottom: 2px solid $monday;
    }
    &--color2:focus {
      border-bottom: 2px solid $tuesday;
    }
    &--color3:focus {
      border-bottom: 2px solid $wednesday;
    }
    &--color4:focus {
      border-bottom: 2px solid $thursday;
    }
    &--color5:focus {
      border-bottom: 2px solid $friday;
    }
    &--color6:focus {
      border-bottom: 2px solid $saturday;
    }
  }

  &__btn {
    font-size: 20px;
  }
}

@media (min-width: 768px) {
  .todo__wrapper {
    width: 80%;
  }

  .todo__list {
    height: 45vh;
  }
}

@media (max-width: 767px) {
  .todo__wrapper {
    width: 100%;
  }

  .todo__list {
    height: 50vh;
  }
}

@media (min-width: 426px) {
  .todo {
    height: 85%;
  }

  .todo__list {
    width: 60%;
  }
}

@media (max-width: 425px) {
  .todo {
    height: 100%;
  }

  .todo__list {
    width: 95%;
  }
}
</style>