<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">


          <Message v-if="message" :message="message"/>

          <NewNote :note="note" @addNote="addNote"/>

          <div class="note-header">
            <h1>{{ title }}</h1>
            <Search placeholder="Find your note" :value="search" @search="search = $event"/>
            <div class="icons" style="">
              <svg :class="{active: grid}" @click="grid = true" style="cursor: pointer"
                   xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                   stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <rect x="3" y="3" width="7" height="7"></rect>
                <rect x="14" y="3" width="7" height="7"></rect>
                <rect x="14" y="14" width="7" height="7"></rect>
                <rect x="3" y="14" width="7" height="7"></rect>
              </svg>
              <svg :class="{active: !grid}" @click="grid = false" style="cursor: pointer"
                   xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                   stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <line x1="8" y1="6" x2="21" y2="6"></line>
                <line x1="8" y1="12" x2="21" y2="12"></line>
                <line x1="8" y1="18" x2="21" y2="18"></line>
                <line x1="3" y1="6" x2="3" y2="6"></line>
                <line x1="3" y1="12" x2="3" y2="12"></line>
                <line x1="3" y1="18" x2="3" y2="18"></line>
              </svg>
            </div>
          </div>

          <Notes :notes="notesFilter" @remove="removeNote" @change="changeNote" :grid="grid"/>

        </div>
      </section>

    </div>
  </div>

</template>

<script>

import Message from './components/Message.vue'
import NewNote from './components/NewNote.vue'
import Notes from './components/Notes.vue'
import Search from './components/Search.vue'

export default {
  components: {
    Message,
    NewNote,
    Notes,
    Search,

  },
  data() {
    return {
      title: 'Notes App',
      message: null,
      grid: true,

      search: '',
      note: {
        title: '',
        descr: '',
        easy: false,
        normal: false,
        hard: false,
        changing: false,
      },
      notes: [
        {
          title: 'First note',
          descr: 'Description for first note',
          date: new Date(Date.now()).toLocaleString(),
          easy: false,
          normal: true,
          hard: false,
          changing: false,
        },
        {
          title: 'Second note',
          descr: 'Description for second note',
          date: new Date(Date.now()).toLocaleString(),
          easy: true,
          normal: false,
          hard: false,
          changing: false,
        },
        {
          title: 'Third note',
          descr: 'Description for third note',
          date: new Date(Date.now()).toLocaleString(),
          easy: false,
          normal: false,
          hard: true,
          changing: false,
        },
      ]

    }
  },
  computed: {
    notesFilter() {
      let array  = this.notes,
          search = this.search
      if (!search) return array
      search = search.trim().toLowerCase()
      array = array.filter(function (item) {
        if (item.title.toLowerCase().indexOf(search) !== -1)
          return item
      })
      return array

    }
  },
  methods: {
    addNote() {
      let {title, descr, easy, normal, hard} = this.note

      if (title === '') {
        this.message = 'title can`t be blank!'
        return false
      }
      console.log(this.note)
      this.notes.push({
        title,
        descr,
        date: new Date(Date.now()).toLocaleString(),
        easy,
        normal,
        hard,
        changing: false,
      })
      this.message = null
      this.note.title = ''
      this.note.descr = ''
      this.note.easy = false
      this.note.normal = false
      this.note.hard = false
    },
    removeNote(index) {
      this.notes.splice(index, 1)
    },
    changeNote(index){

this.notes[index.index].title = index.value
      this.notes[index.index].changing = false
    }
  }
}
</script>

<style>

</style>
