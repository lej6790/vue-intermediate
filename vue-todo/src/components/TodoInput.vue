<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <i class="fa-solid fa-plus addBtn"></i>
        </span>

        <Teleport to="body">
        <!-- use the modal component, pass in the prop -->
            <ModalView :show="showModal">
                <template #header>
                    <h3>
                        경고!
                        <i class="closeModalBtn fa-solid fa-square-xmark" @click="showModal = false"></i>
                    </h3>
                </template>
                <template #body>
                    <div>아무것도 입력하지 않으셨습니다.</div>
                </template>
            </ModalView>
        </Teleport>
    </div>
</template>

<script>
import ModalView from './common/ModalView.vue'

export default {
    data() {
        return {
            newTodoItem: "",
            showModal: false
        };
    },
    methods: {
        addTodo() {
            if (this.newTodoItem !== '') {
                this.$store.commit('addOneItem', this.newTodoItem);
                this.clearInput();
            } else {
                this.showModal = !this.showModal;
            }
        },
        clearInput() {
            this.newTodoItem = '';
        }
    },
    components: {
        ModalView
    }
}
</script>

<style scoped>
input:focus {
    outline: none;
}
.inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input {
    border-style: none;
    font-size: 0.9rem;
}
.addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn {
    color: white;
    vertical-align: middle;
}
.closeModalBtn {
    color: #42b983;
}
</style>