<template >
    <div class="container my-3" id="app" style="max-width:50%">
        <div class="input-group mb-3">
            <div class="input-group-prepend"><span class="input-group-text" id="basic-addon1">待辦事項</span></div>
            <input class="form-control" type="text" placeholder="準備要做的任務" v-model.trim="newToDo"
                @keyup.enter="addToDo" />
            <div class="input-group-append">
                <button class="btn btn-success" type="button" @click="addToDo">新增</button>
            </div>
        </div>
        <div class="card text-center">
            <div class="card-header">
                <ul class="nav nav-tabs card-header-tabs">
                    <li class="nav-item" v-for="(item, index) in toDoState" :key="index"><a class="nav-link" href="#"
                            :class="{ 'active': state == item.value }" @click="state = item.value"
                            style="color:#198754;">{{
                                    item.name
                            }}</a></li>
                </ul>
            </div>
            <ul class="list-group list-group-flush text-left">
                <li class="list-group-item" v-for="(item) in toDoFilter" :key="item.id">
                    <div class="d-flex">
                        <div class="form-check">
                            <input class="form-check-input" :id="item.id" type="checkbox"
                                @click="changeComplated(item.id)" v-model="item.completed" />
                            <label class="form-check-label" :for="item.id" :class="{ 'completed': item.completed }">{{
                                    item.title
                            }}({{ item.completed ? '已完成' : '進行中' }})</label>
                        </div>
                        <a class="remove" href="#" @click="removeToDo(item)" style="position: absolute; left:95%">x</a>
                    </div>
                </li>
            </ul>
            <div class="card-footer d-flex justify-content-between">{{ `還有${toDoLength}筆任務未完成` }}<a class="removeAll"
                    href="" @click="cleanToDo">清除所有任務</a></div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            newToDo: "",
            toDo: [],
            toDoState: [
                { name: "全部", value: "all" },
                { name: "進行中", value: "active" },
                { name: "已完成", value: "completed" }
            ],
            state: "all",
        }
    },
    methods: {
        addToDo() {
            let data = {
                id: Math.floor(Date.now()),
                title: this.newToDo,
                completed: false
            }
            console.log("data = ", data)
            this.toDo.push(data)
            this.newToDo = ""
        },
        removeToDo(item) {
            this.toDo.splice(this.getIndex(item.id), 1)
        },
        cleanToDo() {
            this.toDo.splice(0, this.toDo.length)
        },
        getIndex(id) {
            return this.toDo.findIndex((e) => e.id == id)
        },
        changeComplated(id) {
            let index = this.getIndex(id)
            this.toDo[index].completed = !this.toDo[index].completed
        }
    },
    computed: {
        toDoFilter() {
            switch (this.state) {
                case "all":
                    return this.toDo.filter((item) => true)
                case "active":
                    return this.toDo.filter((item) => !item.completed)
                case "completed":
                    return this.toDo.filter((item) => item.completed)
            }
        },
        toDoLength() {
            return this.toDo.filter((item) => !item.completed).length
        }
    }
}
</script>

<style>
.completed {
    text-decoration: line-through;
}

.remove {
    text-decoration: none;
    color: #6f7275;
}

.removeAll {
    text-decoration: none;
    color: #198754;
}
</style>






