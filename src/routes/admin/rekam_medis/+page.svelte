<script>
	import '../../../app.css';
	import Listt from './list.svelte';
	import Add from './add.svelte';
	import { onMount } from 'svelte';

	var response = {
		name: '',
		role: '',
		token: ''
	};

	let dataPasien;

	onMount(() => {
		const url = new URL(window.location.href);
		const message = url.searchParams.get('message');

		fetch('http://localhost:8080/api/users/current', {
			method: 'GET',
			headers: {
				'Content-type': 'application/json',
				'Access-Control-Allow-Origin': '*',
				'Access-Control-Allow-Methods': 'GET, POST, DELETE',
				'X-API-TOKEN': `${message}`
			}
		})
			.then((res) => res.json())
			.then((data) => {
				response = data.data;
				console.log(data);
			})
			.catch((err) => console.log(err));

	});

	let openRm = false;
	let openInv = false;

	function toggleRm() {
		openRm = !openRm;
	}

	function toggleInv() {
		openInv = !openInv;
	}

	let page = 'list';

	function listHandler() {
		page = 'list';
	}

	function addHandler() {
		page = 'add';
	}

	const logoutHandle = async () => {
		const url = new URL(window.location.href);
		const message = url.searchParams.get('message');

		fetch('http://localhost:8080/api/auth/logout', {
			method: 'DELETE',
			headers: {
				'Content-type': 'application/json',
				'Access-Control-Allow-Origin': '*',
				'Access-Control-Allow-Methods': 'GET, POST, DELETE',
				'X-API-TOKEN': `${message}`
			}
		})
			.then((res) => res.json())
			.then((data) => {
				location.href = '/';
			})
			.catch((err) => console.log(err));
	};
</script>

<div class="flex h-screen bg-gray-200">
	<!-- Sidebar -->
	<div class="bg-[#1C2434] text-white w-64 fixed h-full z-10">
		<!-- Logo -->
		<div class="flex items-center justify-center py-4">
			<img src="../../Logo_Klinik.png" alt="Logo" class="h-16 w-15" />
		</div>

		<!-- Menu -->
		<nav class="mt-6">
			<a
				href="/admin?message={response.token}"
				class="py-2 px-4 hover:bg-gray-700 flex items-center"
			>
				<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-9" viewBox="0 0 1024 1024"
					><path
						fill="currentColor"
						d="M924.8 385.6a446.7 446.7 0 0 0-96-142.4a446.7 446.7 0 0 0-142.4-96C631.1 123.8 572.5 112 512 112s-119.1 11.8-174.4 35.2a446.7 446.7 0 0 0-142.4 96a446.7 446.7 0 0 0-96 142.4C75.8 440.9 64 499.5 64 560c0 132.7 58.3 257.7 159.9 343.1l1.7 1.4c5.8 4.8 13.1 7.5 20.6 7.5h531.7c7.5 0 14.8-2.7 20.6-7.5l1.7-1.4C901.7 817.7 960 692.7 960 560c0-60.5-11.9-119.1-35.2-174.4M761.4 836H262.6A371.12 371.12 0 0 1 140 560c0-99.4 38.7-192.8 109-263c70.3-70.3 163.7-109 263-109c99.4 0 192.8 38.7 263 109c70.3 70.3 109 163.7 109 263c0 105.6-44.5 205.5-122.6 276M623.5 421.5a8.03 8.03 0 0 0-11.3 0L527.7 506c-18.7-5-39.4-.2-54.1 14.5a55.95 55.95 0 0 0 0 79.2a55.95 55.95 0 0 0 79.2 0a55.87 55.87 0 0 0 14.5-54.1l84.5-84.5c3.1-3.1 3.1-8.2 0-11.3zM490 320h44c4.4 0 8-3.6 8-8v-80c0-4.4-3.6-8-8-8h-44c-4.4 0-8 3.6-8 8v80c0 4.4 3.6 8 8 8m260 218v44c0 4.4 3.6 8 8 8h80c4.4 0 8-3.6 8-8v-44c0-4.4-3.6-8-8-8h-80c-4.4 0-8 3.6-8 8m12.7-197.2l-31.1-31.1a8.03 8.03 0 0 0-11.3 0l-56.6 56.6a8.03 8.03 0 0 0 0 11.3l31.1 31.1c3.1 3.1 8.2 3.1 11.3 0l56.6-56.6c3.1-3.1 3.1-8.2 0-11.3m-458.6-31.1a8.03 8.03 0 0 0-11.3 0l-31.1 31.1a8.03 8.03 0 0 0 0 11.3l56.6 56.6c3.1 3.1 8.2 3.1 11.3 0l31.1-31.1c3.1-3.1 3.1-8.2 0-11.3zM262 530h-80c-4.4 0-8 3.6-8 8v44c0 4.4 3.6 8 8 8h80c4.4 0 8-3.6 8-8v-44c0-4.4-3.6-8-8-8"
					/></svg
				>

				<span>Dashboard</span>
			</a>
			<button
				on:click={toggleRm}
				class="flex w-full items-center justify-between py-2 px-4 hover:bg-gray-700 focus:outline-none"
			>
				<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" viewBox="0 0 24 24"
					><path
						fill="currentColor"
						fill-rule="evenodd"
						d="M8.962 18.469C6.019 16.214 2 12.489 2 8.967C2 3.083 7.5.886 12 5.43C16.5.886 22 3.083 22 8.967c0 3.522-4.02 7.247-6.962 9.502C13.706 19.489 13.04 20 12 20c-1.04 0-1.706-.51-3.038-1.531M16.5 6.25a.75.75 0 0 1 .75.75v1.25h1.25a.75.75 0 0 1 0 1.5h-1.25V11a.75.75 0 0 1-1.5 0V9.75H14.5a.75.75 0 0 1 0-1.5h1.25V7a.75.75 0 0 1 .75-.75"
						clip-rule="evenodd"
					/></svg
				>
				<span>Rekam Medis</span>
				<svg
					class="h-5 w-5"
					fill="none"
					viewBox="0 0 24 24"
					stroke="currentColor"
					class:rotate={toggleRm}
				>
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"
					></path>
				</svg>
			</button>
			{#if openRm}
				<!-- Dropdown items -->
				<div class="ml-2">
					<a
						href="/admin/rekam_medis?message={response.token}"
						on:click={listHandler}
						class="block py-2 px-4 hover:bg-gray-700">List</a
					>
					<a
						href="/admin/rekam_medis?message={response.token}"
						on:click={addHandler}
						class="block py-2 px-4 hover:bg-gray-700">Add</a
					>
				</div>
			{/if}

			<button
				on:click={toggleInv}
				class="flex w-full items-center justify-between py-2 px-4 hover:bg-gray-700 focus:outline-none"
			>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
					><path
						fill="currentColor"
						d="m15.5 19.925l-4.25-4.25l1.4-1.4l2.85 2.85l5.65-5.65l1.4 1.4zM21 10h-2V5h-2v3H7V5H5v14h6v2H5q-.825 0-1.412-.587T3 19V5q0-.825.588-1.412T5 3h4.175q.275-.875 1.075-1.437T12 1q1 0 1.788.563T14.85 3H19q.825 0 1.413.588T21 5zm-9-5q.425 0 .713-.288T13 4q0-.425-.288-.712T12 3q-.425 0-.712.288T11 4q0 .425.288.713T12 5"
					/></svg
				>
				<a href="/admin/inventory?message={response.token}"><span>Inventory Obat</span></a>
				<svg
					class="h-5 w-5"
					fill="none"
					viewBox="0 0 24 24"
					stroke="currentColor"
					class:rotate={toggleInv}
				>
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"
					></path>
				</svg>
			</button>
			{#if openInv}
				<!-- Dropdown items -->
				<div class="ml-2">
					<a
						href="/admin/inventory?message={response.token}"
						class="block py-2 px-4 hover:bg-gray-700">list</a
					>
					<a
						href="/admin/inventory?message={response.token}"
						class="block py-2 px-4 hover:bg-gray-700">Add</a
					>
				</div>
			{/if}
		</nav>
	</div>

	<!-- Main Content -->
	<div class="flex-1 overflow-y-scroll">
		<!-- Navbar -->
		<nav class="bg-[#FFF] text-black p-4 shadow-sm">
			<div class="flex items-center justify-end space-x-6">
				<div>
					<p class="px-3 py-1 text-right">{response.name} <br /> Admin</p>
				</div>
				<button on:click={logoutHandle} class="btn bg-red-600 text-white">Logout</button>
			</div>
		</nav>

		<!-- Main Content -->
		{#if page == 'list'}
			<Listt />
		{:else if page == 'add'}
			<Add />
		{:else}
			<h1>Empty</h1>
		{/if}
	</div>
</div>
