<template>
    <div class="text-center">
        <button class="btn w-25 mt-3" style="background:#333;color:#fff;" @click="$emit('clear-todo')">Clear Todos</button>
    </div>
</template>

<script>

export default {
    name: 'ClearTodo',
    emits: ['clear-todo']
}
</script>
