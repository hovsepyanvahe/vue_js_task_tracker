<template>
    <div class="container">
        <MainHeader @toggle-add-task="toggleAddTask"
         title="Task tracker"
         :showAddTask="showAddTask" />
        <div v-show="showAddTask">
            <AddTask @add-task="addTask" />
        </div>
        <MainTasks
            @toggle-reminder="toggleReminder"
            @delete-task="deleteTask"
            :tasks="tasks"
        />
    </div>
</template>

<script>
import MainHeader from "./components/Header";
import MainTasks from "./components/Tasks";
import AddTask from "./components/AddTask";

export default {
    name: "App",
    components: {
        MainHeader,
        MainTasks,
        AddTask,
    },
    data() {
        return {
            tasks: [],
            showAddTask: false,
        };
    },
    methods: {
        addTask(task) {
            this.tasks = [...this.tasks, task];
            this.showAddTask = false
        },        
        toggleAddTask() {
            this.showAddTask = !this.showAddTask
        },
        deleteTask(id) {
            if (confirm("Are you sure?")) {
                this.tasks = this.tasks.filter((task) => task.id != id);
            }
        },
        toggleReminder(id) {
            this.tasks = this.tasks.map((task) =>
                task.id === id ? { ...task, reminder: !task.reminder } : task
            );
        },
    },
    created() {
        this.tasks = [
            {
                id: 1,
                text: "Doctors Appointment",
                day: "March 1st at 4:30pm",
                reminder: true,
            },
            {
                id: 2,
                text: "Gym",
                day: "March 2nd at 2:30pm",
                reminder: false,
            },
            {
                id: 3,
                text: "Work",
                day: "March 3rd at 1:00pm",
                reminder: true,
            },
        ];
    },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: "Poppins", sans-serif;
}

.container {
    max-width: 500px;
    margin: 30px auto;
    overflow: auto;
    min-height: 300px;
    border: 1px solid steelblue;
    padding: 30px;
    border-radius: 5px;
}

.btn {
    display: inline-block;
    background: #000;
    color: #fff;
    border: none;
    padding: 10px 20px;
    margin: 5px;
    border-radius: 5px;
    cursor: pointer;
    text-decoration: none;
    font-size: 15px;
    font-family: inherit;
}

.btn:focus {
    outline: none;
}

.btn:active {
    transform: scale(0.98);
}

.btn-block {
    display: block;
    width: 100%;
}
</style>
