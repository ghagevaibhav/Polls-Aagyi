<script>
    export let type = 'primary';
    export let flat = false;
    export let inverse = false;
</script>

<button class={type} class:flat={flat} class:inverse={inverse} on:click>
    <slot>
    </slot>
</button>

<style>
button{
    margin-top: 14px;
    border: 0;
    cursor: pointer;
    padding: 8px 12px;
    border-radius: 6px;
    font-weight: bold;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.2);
}
.primary{
    background: #d91b42;
    color: white;
}
.secondary{
    background: #45c496;
    color: white;
}
.flat{
    box-shadow: none;
}
.primary.inverse{
    background: white;
    color: #d91b42;
    border: 2px solid #d91b42;
}

.secondary.inverse{
    background: white;
    color: #45c496;
    border: 2px solid #45c496;
}
</style>