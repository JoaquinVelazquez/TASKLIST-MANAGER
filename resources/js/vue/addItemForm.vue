<template>
    <div class="addItem">
        <h3 class="taskname">Task Name:</h3>
        <input type="text" v-model="item.name" />
        <font-awesome-icon
            icon="plus-square"
            @click="addItem()"
            @keyup.enter="addItem()"
            :class="[item.name ? 'active' : 'inactive', 'plus']"
        />
    </div>
</template>

<script>

export default {
    data:function () {
        return {
            item: {
                name: ""
            }
        }
    },
    methods: {
        addItem() {
            if (this.item.name == '') {
                return;
            }

            axios.post('api/item/store', {
                item: this.item
            })
            .then (response => {
                if (response.status == 201) {
                    this.item.name = "";
                    this.$emit('reloadlist');
                }
            })
            .catch (error => {
                console.log(error);
            })
        }
    }
}

</script>

<style scoped>
.addItem {
    display: flex;
    justify-content: center;
    align-items: center;
}

.taskname {
    margin-right: 10px;
}

input {
    background: #f7f7f7;
    border: none;
    outline: none;
    padding: 5px;
    margin-right: 10px;
    width: 50%;
}

.plus {
    font-size: 20px;
}

.active {
    color: #00CE25;
}

.active:hover {
    font-size: 25px;
    transition: .3s;
    cursor: pointer;
}
.inactive {
    color: #999999;
}
</style>