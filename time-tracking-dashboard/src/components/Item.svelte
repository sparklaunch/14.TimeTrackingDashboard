<script lang="ts">
    export let item;
    export let design;
    export let time;
    let isMouseOverEllipsis: Boolean = false;
    let isMouseOverDetail: Boolean = false;
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
    type Void = void;
    const ellipsisMouseEnterHandler: () => Void = () => {
        isMouseOverEllipsis = true;
    };
    const ellipsisMouseLeaveHandler: () => Void = () => {
        isMouseOverEllipsis = false;
    };
    const detailMouseEnterHandler: () => Void = () => {
        isMouseOverDetail = true;
    };
    const detailMouseLeaveHandler: () => Void = () => {
        isMouseOverDetail = false;
    };
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
    <div
        class="item-detail"
        on:mouseenter|stopPropagation={detailMouseEnterHandler}
        on:mouseleave|stopPropagation={detailMouseLeaveHandler}
        class:detail-hovered={isMouseOverDetail}
    >
        <div class="item-detail-title">
            <p>{item.title}</p>
            <img
                src="/assets/icon-ellipsis.svg"
                alt="Ellipsis"
                on:mouseenter={ellipsisMouseEnterHandler}
                on:mouseleave={ellipsisMouseLeaveHandler}
                class:ellipsis-hovered={isMouseOverEllipsis}
            />
        </div>
        <div class="item-detail-figure">
            <p>{item.timeframes[time].current}hrs</p>
        </div>
        <div class="item-detail-last">
            <p>Last Week - {item.timeframes[time].previous}hrs</p>
        </div>
    </div>
</div>

<style>
    .item {
        border-radius: 10px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        overflow: hidden;
    }
    .item > img {
        width: 80px;
        align-self: flex-end;
        position: relative;
        right: 10px;
        bottom: 10px;
    }
    .item-detail {
        display: flex;
        flex-direction: column;
        background-color: rgb(27, 29, 66);
        border-radius: 10px;
        padding: 25px;
        margin-top: -70px;
        z-index: 1;
        transition: background-color 0.3s;
        cursor: pointer;
    }
    .item-detail-title {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
    .item-detail-title > p {
        color: white;
    }
    .item-detail-title > img {
        width: 15px;
        cursor: pointer;
        transition: filter 0.3s;
    }
    .item-detail-figure {
        margin-bottom: 10px;
    }
    .item-detail-figure > p {
        color: white;
        font-size: 48px;
        font-weight: 300;
    }
    .item-detail-last > p {
        color: rgb(192, 196, 255);
        font-weight: 300;
        font-size: 14px;
    }
    .ellipsis-hovered {
        filter: brightness(1.5);
    }
    .detail-hovered {
        background-color: rgb(45, 50, 112);
    }
    @media all and (max-width: 1440px) {
        .item {
            margin: 30px auto;
        }
        .item > img {
            height: 120px;
            width: auto;
        }
        .item-detail {
            display: block;
        }
        .item-detail-figure {
            flex: none;
            float: left;
            margin-bottom: 0;
        }
        .item-detail-figure > p {
            font-size: 36px;
        }
        .item-detail-last {
            flex: none;
            float: right;
            line-height: 43px;
        }
    }
</style>
