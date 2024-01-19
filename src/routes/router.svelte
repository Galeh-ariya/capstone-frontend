<script>
	import { Router, Route } from 'svelte-routing';
    import login from './login/+page.svelte';
    import home from './+page.svelte';
    import rm from './rm/+page.svelte';
    import admin from './admin/+page.svelte';
</script>

<Router>
	<Route path="/" component={home} />
	<Route path="/about" component={login} />
	<Route path="/rm" component={rm} />
	<Route path="/admin" component={admin} />
	
	<!-- ... tambahkan rute lainnya sesuai kebutuhan -->
</Router>
