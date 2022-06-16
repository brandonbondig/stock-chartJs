<template>
    <div class="container" @click="isOpen = !isOpen">
        <div class="sidiv" :class="{ active: isOpen }"></div>

        <p class="dropdown">{{ title }}</p>
        <div v-if="isOpen">
            <p v-for="item in items" @click="changeTitle(item.object); emitTitle()">
                {{ item.object }}
            </p>
        </div>

    </div>
</template>

<script>
export default {
    name: 'dropdown',
    props: ['title', 'items', 'name'],
    data() {
        return {
            isOpen: false,
            title: this.name,
            id: null
        }
    },
    methods: {
        changeTitle: function (title) {
            this.title = title
        },
        emitTitle() {
            this.$emit("emitTitle", this.title);
        },
    },
    mounted() {
        this.id = this._uid
    }
}
</script>

<style scoped lang="scss">
p {
    color: white;
    cursor: pointer;
}

p:not(.dropdown) {
    margin: 2px;
    border-style: solid;
    border-color: #393939;
    border-width: 1px;
    border-bottom: 0px;
    border-left: 0px;
    border-right: 0px;
    font-weight: normal !important;

}

p:not(.dropdown):hover {
    color: #ff4343;
}

.dropdown {
    cursor: pointer;
    user-select: none;
    margin: 0;
    padding: 5px;
    font-weight: bold;

}

.container {
    width: 75%;
    margin: auto;
    border-radius: 15px;
    background-color: #444444;
}



.sidiv {
    position: absolute;
    border-left: 7px solid transparent;
    border-right: 7px solid transparent;
    border-bottom: 7px solid rgb(245, 245, 245);
    width: 5px;
    margin-top: 15px;
    margin-left: 80%;
    transform: rotate(180deg);

}



.active {
    transform: rotate(0deg);
}
</style>