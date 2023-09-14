<script>
    import {onMount} from "svelte";
    import {useSWR} from "sswr";
    // Call the `useSWR` and pass the key you want to use. It will be pased
    // to the fetcher function. The fetcher function can be configured globally
    // or passed as one of the options to this function.

    async function fetchData2() {
        const response = await fetch('https://jsonplaceholder.typicode.com/users');

        const users = await response.json();

        if (response.ok) {
            return users;
        } else {
            throw new Error(response.statusText);
        }
    }

    const {data: users3, error: error3, isLoading: isLoading3} = useSWR("https://jsonplaceholder.typicode.com/users");

</script>

<div>
    {#if $isLoading3}
        <div>Loading...</div>
    {/if}

    {#if $users3}
        <ul>
            {#each $users3 as user}
                <li>{user.name}</li>
            {/each}
        </ul>
    {/if}

    {#if $error3}
        <div>{$error3}</div>
    {/if}
</div>

<!--<div>-->
<!--    {#await fetchData2()}-->
<!--        <div>Loading...</div>-->
<!--    {:then users}-->
<!--        <ul>-->
<!--            {#each users as user}-->
<!--                <li>{user.name}</li>-->
<!--            {/each}-->
<!--        </ul>-->
<!--    {:catch error}-->
<!--        <p>Sorry, there was an error</p>-->
<!--    {/await}-->
<!--</div>-->

<!--<div>-->
<!--    {#if users}-->
<!--        <ul>-->
<!--            {#each users as user}-->
<!--                <li>{user.name}</li>-->
<!--            {/each}-->
<!--        </ul>-->
<!--    {:else if error}-->
<!--        <p>{error}</p>-->
<!--    {:else}-->
<!--        <div>Loading...</div>-->
<!--    {/if}-->
<!--</div>-->