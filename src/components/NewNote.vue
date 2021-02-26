<template>
  <div>
    <div class="new-note">
      <label class="title">Title</label>
      <input type="text" v-model="note.title">
      <label class="title" style="margin-top: 20px;">Importance</label>
      <p><input type="radio" name="Importance" id="easy" v-model="note.easy" v-bind:value="true" @change="changeNH"
                checked>Обычное</p>
      <p><input type="radio" name="Importance" id="normal" v-model="note.normal" v-bind:value="true" @change="changeEH">Важное
      </p>
      <p><input type="radio" name="Importance" id="hard" v-model="note.hard" v-bind:value="true" @change="changeEN">Очень
        важное</p>
      <label class="title">Description</label>
      <textarea v-model="note.descr"></textarea>
      <button class="btn btnPrimary" @click="addNote">New note</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      required: true,
    },
  },

  methods: {
    addNote() {

      this.$emit('addNote', this.note)

    },
    changeEH() {
      this.note.easy = false
      this.note.hard = false
    },
    changeEN() {
      this.note.easy = false
      this.note.normal = false
    },
    changeNH() {
      this.note.normal = false
      this.note.hard = false
    },
  },
}
</script>

<style scoped>
label {
  margin-bottom: 30px;
}

.new-note {
  text-align: center;
}

.btn {
  margin: 20px 0 20px 0;
}

p {

  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 40px;

}

p:last-child {
  margin-right: 0;

}

p:first-child {

}

input {
  margin-bottom: 0;
}

.title {
  font-weight: bold;
}

</style>