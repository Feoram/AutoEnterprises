<script>
    import {Route, Router, useLocation} from "svelte-routing";
    import Layout from "./lib/Layout/__layout.svelte";
    import Registration from "./lib/Components/Authorization/Registration.svelte";
    import CreateForm from "./lib/Routes/CreateForm.svelte";
    import EditingForm from "./lib/Routes/EditingForm.svelte";
    import Statistics from "./lib/Routes/Statistics.svelte";
    import Settings from "./lib/Routes/Settings.svelte";

    // Получаем текущий маршрут
    const location = useLocation();

    // Пути, на которых меню должно быть скрыто
    const authPaths = ["/"];
    let currentPath = window.location.pathname;
</script>

<Router>
    {#if !authPaths.includes(currentPath)}
        <Layout>
            <Route path="/home" component={CreateForm}/>
            <Route path="/editing" component={EditingForm}/>
            <Route path="/stats" component={Statistics}/>
            <Route path="/settings" component={Settings}/>

        </Layout>
    {/if}

    <Route path="/" component={Registration} />
</Router>
