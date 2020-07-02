<template>
    <div class="item-list">
        <input type="checkbox"
        class="toggle"
        v-model="todo.completed">
        <label>{{todo.content}}</label>
        <button
        class="destory" @click="deleteTodo">X</button>
    </div>
</template>

<script>
export default {
    data() {
        return {

        }
    },
    props: {
        todo: {
            type: Object,
            required: true
        }
    },
    methods: {
        deleteTodo() {
            this.$emit('dev', this.todo.id)
        }
    }
}
</script>
<style lang="stylus" scoped>
    .item-list {
        width 100%
        height 38px
        background-color #ddd5d5
        box-shadow 3px 3px #7b7b7b
        position relative
    }
    .toggle {
        width 20px
        height 20px
        margin 10px
    }
    label {
        position absolute
        margin 10px
        width 380px
        font-size 18px
        color black
        font-weight 500

    }
    .destory {
        float right
        margin 5px
        border-radius 5px
    }

</style>