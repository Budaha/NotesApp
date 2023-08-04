<template>
    <div class="wrapper">
        <div class="wrapper-content">
            <section>
                <div class="container">
                    <!--message-->
                    <message-component v-if="message" :message="message"/>
                    <!--new note-->
                    <new-note :note="note" @addNote="addNote" />
                    <div class="note-header" style="margin: 36px 0;">
                    <!--title-->
                    <h1> {{ title }}</h1>
                    <!--search-->
                    <search-component :value="search"
                        placeholder="Find your note"
                        @search="search = $event"/>   
                    <!--icons controls-->   
                        <div class="icons">
                            <svg :class="{ active: grid }" @click="grid = true" style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
                            <svg :class="{ active: !grid }" @click="grid = false" style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
                        </div>
                    </div>
                   <!--note list-->
                    <notes-component :notes="notesFilter" :grid="grid" @remove="removeNote"/>
                </div>   
            </section>
        </div>
    </div>    
</template>


<script>
import messageComponent from '@/components/Message.vue'
import notesComponent from '@/components/Notes.vue'
import newNote from '@/components/NewNote.vue'
import searchComponent from '@/components/Search.vue'
export default {
    components: {
        messageComponent, notesComponent, newNote, searchComponent
},
    data() {
        return {
            title: 'Notes app',
            search: '',
            message: null,
            grid: true,
            note: {
                title: '',
                description: '',
                select: ''
            },
            notes: [
                {
                    title: 'First note',
                    description: 'Description for first note',
                    date: new Date(Date.now()).toLocaleString()
                },
                {
                    title: 'Second note',
                    description: 'Description for second note',
                    date: new Date(Date.now()).toLocaleString()
                },
                {
                    title: 'Third note',
                    description: 'Description for third note',
                    date: new Date(Date.now()).toLocaleString()
                }

            ]
        }
    },
    computed: {
        notesFilter () {
            let array = this.notes,
                search = this.search
            if (!search) return array
            search = search.trim().toLowerCase()
            array = array.filter(function (item) {
               if (item.title.toLowerCase().indexOf(search) !== -1)  {
                return item
               }
            })
            return array
        }
    },
    methods: {
        addNote() {
            let {title, description, select} = this.note

            if (title === '') {
                this.message = 'Заголовок не может быть пустым!'
                return false
            }

            this.notes.push({
                title,
                description,
                date: new Date(Date.now()).toLocaleString(),
                select
            })
            this.message = null
            this.note.title = ''
            this.note.description = ''
            this.note.select = ''
            
        },
        removeNote (index) {
            this.notes.splice(index, 1)
        },
    }

}
</script>