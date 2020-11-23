<template>
    <div :class="item.done?'todo-line':''" @click="changeStatus" v-if="show(item)">
        <span>{{item.text}}</span>
        <button class="del-button" @click="del">删除</button>
    </div>
</template>
<script>
export default {
    name: 'TodoItem',
    props: ['item', 'filter'],
    computed: {
        //过滤任务是否显示
        show () {
            return item => {
                if (this.filter == 'all') {
                    return true
                } else {
                    if (this.filter == 'completed') {
                        if (item.done) {
                            return true
                        } else {
                            return false
                        }
                    } else {
                        if (!item.done) {
                            return true
                        } else {
                            return false
                        }
                    }
                }

            }
        }
    },
    methods: {
        //修改任务状态
        changeStatus () {
            this.$emit('on-change')
        },
        //删除任务
        del () {
            this.$emit('on-del')
        }
    }
}
</script>