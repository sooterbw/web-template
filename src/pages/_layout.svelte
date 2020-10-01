<script>
    import { isActive, metatags, page, focus } from '@sveltech/routify'
    import { fly, fade } from 'svelte/transition';
    import { jwt } from '../stores.js';

    let modal = false;
    let edit, settings = false;

    let toTitleCase = (s) => {
        return s.toLowerCase().split(' ').map(w => w[0].toUpperCase() + w.slice(1)).join(' ');
    }

    if($page.title != 'index'){
        metatags.title = `My Website | ${toTitleCase($page.title)}`;
    }

    let logOff = () => jwt.set(false);
    const test = true;
</script>

{#if $jwt && !$isActive('./auth')}
    <div class="admin-panel" out:fly="{{ x:-60, duration:1500 }}">
        <div class="admin-top">
            <p>Logo</p>
            <svg class='admin-icon' fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
            </svg>
        </div>
        <div class="admin-bot">
            <svg class='admin-icon' on:click={() => modal = !modal} fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
            </svg>
            <svg class='admin-icon' on:click={logOff} fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1" />
            </svg>
        </div>
    </div>

    {#if test}
    <div class="test-data" out:fly="{{ x:300, duration:1500 }}">
        <p>{$page.title}</p>
    </div>
    {/if}

    {#if modal}
    <div class="modal-mask">
        <div class="modal" transition:fade={{duration:500}}>
            <svg class="close-modal" on:click={() => modal = false} fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
            <h1>Test Modal!</h1>
        </div>
    </div>
    {/if}
{/if}

<slot />

<style>
    .test-data {
        position: fixed;
        display: flex;
        justify-content: center;
        align-items: center;
        top: 0;
        right: 0;
        background-color: aliceblue;
        width: 15em;
        height: 50px;
        border-radius: 0 0 0 10px;
        font-weight: bold;
    }

    .admin-panel {
        display: flex;
        position: fixed;
        top: 0;
        left: 0;
        height: 100vh;
        width: 3.5em;
        background-color: aliceblue;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
    }

    .admin-icon {
        height: 36px;
        width: 36px;
        padding-bottom: 5px;
        cursor: pointer;
    }

    .admin-icon:hover {
        color: gray;
    }

    .admin-top, .admin-bot {
        display: flex;
        flex-direction: column;
        padding-top: 10px;
    }

    .modal-mask {
        position: absolute;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        width: 100vw;
        background-color: rgba(0,0,0,.5);
    }

    .modal {
        position: relative;
        background-color: aliceblue;
        height: 300px;
        width: 500px;
        border-radius: 10px;
        box-shadow: 2px 2px 5px 2px #0000006b;
    }

    .close-modal {
        position: absolute;
        top: .5em;
        right: .5em;
        height: 1.5em;
        width: 1.5em;
        cursor: pointer;
    }

    .close-modal:hover {
        color: gray;
    }
</style>