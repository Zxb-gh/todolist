<template>
    <button class="filter-ml-20" @click="filter">
        {{item.label}}
    </button>
</template>
<script>
export default {
    name: 'Filter',
    props: ['item'],
    methods: {
        //过滤任务列表
        filter () {
            this.$emit('on-filter')
        }
    }
}
</script>
