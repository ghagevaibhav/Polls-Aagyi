<script>
    import PollStore from '../stores/PollStore.js';
    import PollDetails from './PollDetails.svelte';
    import {fade, slide, scale} from 'svelte/transition';
    import{flip} from 'svelte/animate';
</script>

<div class="poll-list">
    {#each $PollStore as poll (poll.id)}
    <div out:scale|local in:fade animate:flip={{duration: 500}}>
        <PollDetails {poll}  />
    </div>
    {/each}
</div>

<style>
    .poll-list{
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;
    }

</style>