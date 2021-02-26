<template>
  <div>
    <div class="notes">
      <div class="note" :class="{full: !grid, easy: note.easy, normal: note.normal, hard: note.hard}"
           v-for="(note, index) in notes" :key="index">
        <div class="note-header" :class="{full: !grid}">
          <p @click="note.changing = true;
          value = ''"
             class="titleCard">{{ note.title }}
            <input v-model="value" v-show="note.changing"
                   type="text"
                   class="newTitle"
                   @keyup.enter="changeTitle(index, value)"
                   @keyup.esc="note.changing=false"
                   @focusout="note.changing=false">
          </p>


          <p style="cursor: pointer" @click="removeNote(index)">x</p>
        </div>
        <div class="note-body">
          <p>{{ note.descr }}</p>
          <span>{{ note.date }}</span>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      value: ''
    }
  },
  props: {
    notes: {
      type: Array,
      default: '',
      required: true,
    },
    grid: {
      type: Boolean,
      default: '',
      required: true,
    },

  },
  methods: {
    removeNote(index) {
      console.log(`Note ${index} removed`)
      this.$emit('remove', index)
    },

    changeTitle(index, value) {
      this.$emit('change', {index, value})

    }
  },

}
</script>

<style lang="scss">
.notes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;
}

.note {
  width: 49%;
  padding: 18px 20px;
  margin-bottom: 20px;
  background: #fff;
  transition: 0.25s;
}

.note:hover {
  box-shadow: 0 30px 30px rgba(0, 0, 0, 0.04);
  transform: translate(0, -6px);
}

.full {
  width: 100%;
  text-align: center;
}

.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;

  &.full {
    justify-content: center;

    p {
      margin-right: 12px;
    }
  }

  h1 {
    font-size: 32px;
  }

  p {
    font-size: 22px;
    color: #402caf;
  }

  svg {
    margin-right: 12px;
    color: #999999;

    &.active {
      color: #402caf;
    }

    &:last-child {
      margin-right: 0;

    }

  }
}

.note-body {
  padding: 20px 0px;

}

span {
  font-size: 14px;
  color: #999999;
}

.hard {
  border: 3px solid red;
}

.easy {
  border: 3px solid green;

}

.normal {
  border: 3px solid yellow;
}

.titleCard {
  position: relative;
}

.newTitle {
  content: '';
  width: 140px;
  height: 40px;
  position: absolute;
  top: 0;
  left: 0;
  border-radius: 0;
  border: 1px solid black;
  z-index: 2;

}

</style>