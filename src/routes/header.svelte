<script lang='ts'>
    import { page } from '$app/stores'
</script>

<header>
    <nav>
        <a class="name" aria-current={$page.url.pathname == '/' ? 'page': undefined} href="/">svelt-rating-selector-display</a>
        <ul>
            <li aria-current={$page.url.pathname == '/demo' ? 'page': undefined}>
                <a href="/demo">Demo</a>
            </li>
            <li aria-current={$page.url.pathname == '/contact' ? 'page': undefined}>
                <a href="/docs">Docs</a>
            </li>
        </ul>
    </nav>
    <div class="icons">
        <a class="icon github" href="https://github.com/stinger567/svelt-rating-selector-display">
            <svg viewBox="-2 -2 28 28"  xmlns="http://www.w3.org/2000/svg">
                <path
                    d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                />
            </svg>
        </a>
    </div>
</header>

<style>
    header {
        display: flex;
        align-items: center;
        background-color: var(--secondary-color-dark);
    }
    
    a{
        text-decoration: none;
    }

    nav {
        flex: 2;
        display: flex;
        flex-wrap: wrap;
        align-items: center;
    }

    ul {
        flex: 1;
        list-style: none;
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 0;
    }

    li {
        font-size: clamp(1rem, 5vw, 2rem);
        padding-top: 0;
        padding-inline: 0.5em;
    }

    li a{
        color: var(--main-color-light);
    }

    li a:hover{
        color: var(--secondary-color-light);
    }

    .name{
        flex: 1;
        white-space: nowrap;
        font-size: clamp(1rem, 5vw, 2rem);
        padding-left: 1em;
        padding-top: 0.5em;
        padding-bottom: 0.5em;
        color: rgb(218, 154, 252);
    }

    .name:hover{
        color: rgb(162, 133, 177);
    }

    .icons {
        flex: 1;
        display: flex;
        justify-content: flex-end;
        padding: 1em;
    }

    svg {
        stroke: var(--main-color-light);
        fill: transparent;
        width: clamp(2.5rem, 10vw, 4rem);
        transition: fill 0.2s ease-in-out;
    }

    svg:hover {
        stroke: var(--secondary-color-light);
        fill: var(--secondary-color-light);
        cursor: pointer;
    }
</style>