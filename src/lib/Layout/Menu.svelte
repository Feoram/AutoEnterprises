<script>
    import { Link } from "svelte-routing";

    const links = [
        { name: 'Create Form', path: '/home' },
        { name: 'Editing Form', path: '/editing' },
        { name: 'Statistics', path: '/stats' },
        { name: 'Settings', path: '/settings' },
    ];
</script>

<nav class="nav-bar">
    {#each links as link}
        <Link to={link.path}>
            <p class="nav-item">{link.name}</p>
        </Link>
    {/each}
</nav>

<style>
    .nav-bar {
        display: flex;
        justify-content: space-around;
        align-items: center;
        background-color: #1e1e1e;
        padding: 20px 0;
        box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.5);
        width: 100%;
        position: fixed;
        top: 0;
        left: 0;
        z-index: 1000;
    }

    .nav-item {
        color: #f0f0f0;
        padding: 10px 30px;
        font-size: 18px;
        font-weight: bold;
        text-transform: uppercase;
        text-decoration: none;
        cursor: pointer;
        border-radius: 6px;
        transition: background-color 0.3s ease, color 0.3s ease, transform 0.2s ease;
    }

    .nav-item:hover {
        background-color: #007BFF;
        color: #fff;
        transform: translateY(-3px);
    }

    .nav-item:active {
        transform: translateY(0);
    }

    .nav-item:focus {
        outline: none;
        box-shadow: 0 0 8px rgba(0, 123, 255, 0.7);
    }
</style>
