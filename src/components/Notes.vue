<template>
    <div class="notes">
        <div class="note" :class="{ full: !grid }" v-for="(note, index) in notes" :key="index">
            <div class="note-header" :class="{ full: !grid }">
                <p>{{ note.title }}</p>  
                <p style="cursor: pointer" @click="removeNote(index)">x</p>   
            </div>
            <div class="note-body">
                <p>{{ note.description }}</p>
                    <div class="note-select">
                        <span>{{ note.date }}</span>
                        <p :class="{warning:  note.select === 'Важная задача' }">{{ note.select }}</p>
                    </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
name: "notesComponent",
props: {
    notes: {
        type: Array,
        required: true
        },
    grid: {
        type: Boolean,
        required: true
        }
    },
methods: {
    removeNote (index) {
    this.$emit('remove', index)
    }
}
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
    width: 48%;
    padding: 18px 20px;
    margin-bottom: 20px;
    background-color: white;
    transition: all .25s cubic-bezier(.02,.01,.47,1);
    box-shadow: 0 30px 30px rgba(0,0,0,.02);
    &:hover {
        box-shadow: 0 30px 30px rgba(0,0,0,.04);
        transform: translate(0,-6px);
        transition-delay: 0s !important;
    }
    &.full {
        width: 100%;
        text-align: center;
    }
}
.note-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
h1 {
    font-size: 32px;   
}
p {
    font-size: 22px;
    color: blue;
    }
svg {
    margin-right: 12px;
    color: gray;
    &.active {
        color: blue;
    }
    &:last-child {
        margin-right: 0;
        }
    }
    &.full {
        justify-content: center;
        p {
            margin-right: 16px;
            &:last-child {
                margin-right: 0;
            }
        }
    }
}
.note-body {
p {
    margin: 20px 0;
}
span {
    font-size: 14px;
    color: gray;
    }
}
.note-select {
    display: flex;
    justify-content: space-between;
    align-items: center;
    p{ 
        margin: 0;
    }

    
    
}
.warning{
    color:red;
}
</style>