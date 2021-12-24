<script lang="ts">
    import Profile from "./components/Profile.svelte";
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
