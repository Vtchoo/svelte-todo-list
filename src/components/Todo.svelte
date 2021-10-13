<script lang="ts">
    export let todo: string
    export let done: boolean
    export let id: string

    export let onSetDone: (id: string, done: boolean) => void
    export let onRemove: (id: string) => void
</script>

<div class="container" class:done>
    <p>{todo}</p>
    <div>
        <button on:click={() => onRemove(id)} class="delete">Excluir</button>
        <button on:click={() => onSetDone(id, !done)}>Finalizada</button>
    </div>
</div>

<style>
    .container {
        background-color: pink;
        display: flex;
        align-items: center;
        padding: .25rem;
    }

    .container.done {
        background-color: lightgreen;
    }

    .container > p {
        flex: 1
    }

    button {
        margin: 0;
    }
    button.delete {
        color: red;
    }

</style>