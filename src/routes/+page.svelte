<script lang="ts">
    type ToDoItem = {
        text: string
        done: boolean
    }
    type Filters = 'all' | 'active' | 'completed'

    let toDoList = $state<ToDoItem[]>([])
    let filter = $state<Filters>('all')
    let filteredList = $derived(filterList())

    $effect(() => {
        const savedToDoList = localStorage.getItem('toDoList') 
        savedToDoList && (toDoList = JSON.parse(savedToDoList)) 
    })

    $effect(() => {
        localStorage.setItem('toDoList', JSON.stringify(toDoList))
    })

    function addToDoItem(event: KeyboardEvent){
        if (event.key !== 'Enter') return

        const toDoElement = event.target as HTMLInputElement
        const text = toDoElement.value
        const done = false

        toDoList = [ ...toDoList, {text, done}]

        toDoElement.value = ''
    }

    function editToDoItem(event: Event) {
        const inputElement = event.target as HTMLInputElement
        const index = +inputElement.dataset.index!
        toDoList[index].text = inputElement.value
    }

    function toggleCheckbox(event: Event){
        const inputElement = event.target as HTMLInputElement
        const index = +inputElement.dataset.index!
        toDoList[index].done = !toDoList[index].done
    }

    function setFilter(newFilter: Filters) {
        filter = newFilter
    }
    
    function filterList() {
        switch (filter) {
            case "all":
                return toDoList
            case "active":
                return toDoList.filter(toDoItem => !toDoItem.done)
            case "completed":
                return toDoList.filter(toDoItem => toDoItem.done)
        }
    }

    function remaining() {
        return toDoList.filter(toDoItem => !toDoItem.done).length
    }
</script>

<input on:keydown={addToDoItem} placeholder="Add new item" type="text" />

<div class="to-do-list">
    {#each filteredList as toDoItem, i}
        <div class:completed={toDoItem.done} class="to-do-item">
            <input on:input={editToDoItem} data-index={i} value={toDoItem.text} type="text">
            <input onchange={toggleCheckbox} data-index={i} checked={toDoItem.done} type="checkbox">
        </div>
    {/each}
</div>

<div class="filters">
    <button onclick={() => setFilter('all')}>All</button>
    <button onclick={() => setFilter('active')}>Active</button>
    <button onclick={() => setFilter('completed')}>Completed</button>
</div>

<p>{remaining()} Remaining</p>

<style>
    .to-do-list {
        display: grid;
        gap: 1rem;
        margin-block-start: 1rem;
    }

    .to-do-item {
        position: relative;
        display: flex;
        transition: opacity 0.3s;
    }

    .completed {
        opacity: 0.4;
    }

    input[type="text"] {
        width: 100%;
        padding: 1rem;
    }

    input[type="checkbox"] {
        position: absolute;
        right: 4%;
        top: 45%;
        translate: 0% -50%;
    }

    .filters {
        margin-block: 1rem;
    }
</style>