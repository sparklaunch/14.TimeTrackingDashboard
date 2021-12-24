<script lang="ts">
    import { onMount } from "svelte";
    import Profile from "./components/Profile.svelte";
    type TimeMarker = {
        current: number;
        previous: number;
    };
    interface TimeFrame {
        daily: TimeMarker;
        weekly: TimeMarker;
        monthly: TimeMarker;
    }
    interface Item {
        title: string;
        timeframes: TimeFrame;
    }
    onMount(async () => {
        const response: Response = await fetch("/data.json");
        const data: Item[] = await response.json();
    });
</script>

<div id="app">
    <div id="container">
        <Profile />
    </div>
</div>

<style>
    #app {
        display: flex;
        height: 100%;
        justify-content: center;
        align-items: center;
    }
    #container {
        display: grid;
        grid-template-areas: "profile work play study" "profile exercise social self-care";
    }
</style>
