<script>
    import Menu from "./Menu.svelte";
</script>

<Menu />
<div class="layout">
    <div class="content">
        <slot />
    </div>
</div>

<style>
    .layout {
        display: flex;
        flex-direction: column;
        min-height: 100vh;
    }

    .content {
        padding-top: 80px;
        flex: 1;
        background-color: #1e1e1e;
        color: #fff;
    }
</style>
