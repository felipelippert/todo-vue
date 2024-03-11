<script setup>
    const props = defineProps(['addTask', 'tempTask', 'changeFilter', 'editTempTask'])
</script>
<template>
    <form @submit.prevent="props.addTask">
        <div class="row">
            <div class="col">
                <input :value="props.tempTask" @change="props.editTempTask" required
                    class="form-control" type="text" placeholder="Type task description here">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Register</button>
            </div>
            <div class="col-md-2">
                <select @change="props.changeFilter" class="form-control">
                    <option value="all">All tasks</option>
                    <option value="pending">Pending tasks</option>
                    <option value="completed">Completed tasks</option>
                </select>
            </div>
        </div>
    </form>
</template>