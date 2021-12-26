<script lang="ts">
    import { onMount } from "svelte";
    import Profile from "./components/Profile.svelte";
    import Item from "./components/Item.svelte";
    let data: Item[] = [];
    type Time = "daily" | "monthly" | "weekly";
    let chosen: Time = "weekly";
    class Color {
        r: Number;
        g: Number;
        b: Number;
        a: Number;
        constructor(r: Number, g: Number, b: Number, a: Number = 1) {
            this.r = r;
            this.g = g;
            this.b = b;
            this.a = a;
        }
        getRGBString: () => String = () => {
            return `rgba(${this.r}, ${this.g}, ${this.b}, ${this.a})`;
        };
    }
    type TimeMarker = {
        current: Number;
        previous: Number;
    };
    interface TimeFrame {
        daily: TimeMarker;
        weekly: TimeMarker;
        monthly: TimeMarker;
    }
    interface Item {
        title: String;
        timeframes: TimeFrame;
    }
    type DesignData = {
        backgroundColor: Color;
        icon: String;
    };
    const designData: DesignData[] = [
        {
            backgroundColor: new Color(255, 128, 89),
            icon: "icon-work.svg"
        },
        {
            backgroundColor: new Color(76, 187, 226),
            icon: "icon-play.svg"
        },
        {
            backgroundColor: new Color(255, 84, 113),
            icon: "icon-study.svg"
        },
        {
            backgroundColor: new Color(65, 201, 119),
            icon: "icon-exercise.svg"
        },
        {
            backgroundColor: new Color(103, 46, 204),
            icon: "icon-social.svg"
        },
        {
            backgroundColor: new Color(239, 191, 80),
            icon: "icon-self-care.svg"
        }
    ];
    const timeChosenHandler = (event) => {
        chosen = event.detail.chosen.toLowerCase();
    };
    onMount(async () => {
        const response: Response = await fetch("/data.json");
        data = await response.json();
    });
</script>

<div id="app">
    <div id="container">
        <Profile on:timeChosen={timeChosenHandler} />
        {#each data as item, index}
            <Item {item} design={designData[index]} time={chosen} />
        {/each}
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
        grid-gap: 30px;
        grid-template-rows: repeat(2, 1fr);
        grid-template-columns: repeat(4, 250px);
    }
    @media all and (max-width: 1440px) {
        #app {
            display: block;
            height: auto;
            padding: 100px 30px;
        }
        #container {
            display: block;
        }
    }
</style>
