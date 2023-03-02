<template>
    <div class="pagination">
        <button v-if="showPrevious" class="item prev" @click="changePage(current - 1)">
            &laquo;
        </button>
        <button v-for="(page, index) in pages" :key="page" class="item" :class="{ current: page === current }"
            @click="changePage(index)"  maxlength="10">
            {{ page }}
        </button>
        <button v-if="showNext" class="item next" @click="changePage(current + 1)">
            &raquo;
        </button>
    </div>
</template>

<script>
export default {
    name: 'PaginationPage',
    props: {
        offset: {
            type: [String, Number],
            default: 0,
        },
        total: {
            type: [String, Number],
            default: 0,
        },
        limit: {
            type: [String, Number],
            required: 50,
        },
    },
    computed: {
        current() {
            return this.offset ? this.offset + 1 : 1;
        },
        pages() {
            const qty = Math.ceil(this.total / this.limit);
            if (qty <= 1) return [1];
            return Array.from(Array(qty).keys(), (i) => i + 1);
        },
    },
    methods: {
        changePage(offset) {
            this.$emit('change-page', offset)
        }
    }
};
</script>


<style  scoped>
.pagination {
    display: flex;
    justify-content: center;
}

.item {
    padding: 0.5rem 0.75rem;
    border: 1px solid orange;
    cursor: pointer;
    background-color: white;
    margin-left: 2px;
    margin-right: 2px;
}

.current {
    cursor: default;
    color: white;
    background-color: orangered;
    border-color: orange;
    z-index: 2;
}
</style>