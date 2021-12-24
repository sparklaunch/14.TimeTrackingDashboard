<script lang="ts">
    import { onMount } from "svelte";
    export let item;
    export let design;
    const extractGridArea: (String) => String = (url: String) => {
        return url.match(/^icon-([a-z\-]+)\.svg$/)[1];
    };
    class Style {
        style: String;
        constructor(styles: Object) {
            let parsed: String = "";
            for (const [key, value] of Object.entries(styles)) {
                parsed += key + ": " + value + ";";
            }
            this.style = parsed;
        }
    }
    $: gridArea = extractGridArea(design.icon);
    $: styleObject = {
        "background-color": design.backgroundColor.getRGBString(),
        "grid-area": gridArea
    };
    $: style = new Style(styleObject);
    $: itemStyle = style.style as string;
</script>

<div class="item" style={itemStyle}>
    <img src="/assets/{design.icon}" alt={item.title} />
</div>
