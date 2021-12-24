<div id="profile">
    <div id="title">
        <img src="/assets/image-jeremy.png" alt="Jeremy" />
        <p>Report for</p>
        <h1>Jeremy Robson</h1>
    </div>
    <ul>
        <li>Daily</li>
        <li class="active">Weekly</li>
        <li>Monthly</li>
    </ul>
</div>

<style>
    #profile {
        grid-area: profile;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }
    #title {
        display: flex;
        flex-direction: column;
        background-color: rgb(77, 62, 231);
        padding: 30px;
        border-radius: 10px;
        margin: -30px -30px 30px -30px;
    }
    #title > img {
        border: 3px solid white;
        border-radius: 50%;
        width: 80px;
        margin-bottom: 30px;
    }
    #title > p {
        color: white;
        opacity: 0.5;
        font-size: 14px;
    }
    #title > h1 {
        color: white;
        font-weight: 300;
        font-size: 36px;
        margin-bottom: 50px;
    }
    #profile {
        background-color: rgb(27, 29, 66);
        padding: 30px;

        border-radius: 10px;
    }
    #profile > ul {
        list-style: none;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }
    #profile > ul > li {
        color: rgb(99, 103, 167);
    }
    #profile > ul > li:not(:last-child) {
        margin-bottom: 20px;
    }
    .active {
        color: white !important;
    }
</style>
