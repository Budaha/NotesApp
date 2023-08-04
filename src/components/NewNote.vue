<template>
    <div class="new-note">
        
        <label>Title</label>
        <input class="title" v-model="noteForm.title" type="text">
        <label>Description</label>
        <textarea class="title" v-model="noteForm.description"></textarea>
        <div class="priority">
            <select class="select" v-model="noteForm.select">
                <option>Стандартная задача</option>
                <option>Важная задача</option>
            </select>
        </div>
        <button class="btn btnPrimary" @click="addNote">New note</button>
        
    </div>
</template>

<script>
export default {
    name: "newNote",
    props: {
        note: {
            type: Object,
            required: true,
        }
    },

    data () {
        return {
            noteForm: this.note,
        }
    },

    methods: {
        addNote() {
            this.$emit('addNote', this.noteForm)
        }
    },
    mounted() {
        this.noteForm = this.note
    }
}
</script>

<style scoped>
.new-note {
    text-align: center; 
}
.priority {
text-align: right;
margin: 15px;
}
.select {
    width: 220px;
    height: 50px;
    text-align: center;
    border: 1px solid #DCDFE6;
    font-size: 18px;
    color: blue;
    border-radius: 20px;
    cursor: pointer;
}
.warning {
    color: red;
}

</style>
