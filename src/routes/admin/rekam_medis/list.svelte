<script>
	import { onMount } from 'svelte';

	/**
	 * @type {any}
	 */
	let dataPasien;

	onMount(() => {
		const url = new URL(window.location.href);
		const message = url.searchParams.get('message');

		fetch('http://localhost:8080/api/users', {
			method: 'GET',
			headers: {
				'Content-type': 'application/json',
				'Access-Control-Allow-Origin': '*',
				'Access-Control-Allow-Methods': 'GET, POST, DELETE'
			}
		})
			.then((res) => res.json())
			.then((data) => {
				dataPasien = data.data;
				console.log(data);
			})
			.catch((err) => console.log(err));
	});

	let data = '';
	const handleInput = async () => {
		fetch(`http://localhost:8080/api/users/search?name=${data}`, {
			method: 'GET',
			headers: {
				'Content-type': 'application/json',
				'Access-Control-Allow-Origin': '*',
				'Access-Control-Allow-Methods': 'GET, POST, DELETE'
			}
		})
			.then((res) => res.json())
			.then((data) => {
				dataPasien = data.data;
				console.log(data);
			})
			.catch((err) => console.log(err));
	};
</script>

<!-- Main Content -->
<div class="flex-1">
	<!-- Main Content -->
	<div class="p-10 ml-60">
		<!-- Your main content here -->
		<h1 class="text-xl font-bold">List Pasien</h1>

		<div class="container flex justify-end">
			<input
				on:input={handleInput}
				bind:value={data}
				type="text"
				placeholder="Type here"
				class="input input-bordered w-22 h-12"
			/>
			<!-- <button class="btn bg-[#66D3D6] text-white font-semibold font-sm">CARI</button> -->
			<button
				><svg xmlns="http://www.w3.org/2000/svg" class="h-11 w-11 mx-2" viewBox="0 0 24 24"
					><path
						fill="currentColor"
						d="M18 7H6V3h12zm0 5.5q.425 0 .713-.288T19 11.5q0-.425-.288-.712T18 10.5q-.425 0-.712.288T17 11.5q0 .425.288.713T18 12.5M16 19v-4H8v4zm2 2H6v-4H2v-6q0-1.275.875-2.137T5 8h14q1.275 0 2.138.863T22 11v6h-4z"
					/></svg
				></button
			>
		</div>

		<div class="container bg-white mt-4 rounded-md">
			<div class="overflow-x-auto">
				<table class="table">
					<!-- head -->
					<thead>
						<tr>
							<th></th>
							<th>No RM</th>
							<th>Nama</th>
							<th>gender</th>
							<th>TTL</th>
							<th>Instansi</th>
							<th>Aksi</th>
						</tr>
					</thead>
					{#if dataPasien}
						{#each dataPasien as pasien, i}
							<tbody class="body">
								<tr class="hover">
									<th>{++i}</th>
									<td>{pasien.noRm}</td>
									<td>{pasien.name}</td>
									<td>{pasien.gender}</td>
									<td>{pasien.tempat_lahir + ', ' + pasien.tanggal_lahir}</td>
									<td>{pasien.instansi}</td>
									<td>
										<a
											href="/admin/rekam_medis/list?rm={pasien.noRm}"
											class="bg-[#FFBE00] p-1 text-white font-semibold rounded-sm">Detail</a
										>
										|
										<a
											href="/admin/rekam_medis/add?rm={pasien.noRm}"
											class="bg-[#00A96E] p-1 text-white font-semibold rounded-sm">Tambah</a
										>
									</td>
								</tr>
							</tbody>
						{/each}
					{/if}
				</table>
			</div>
		</div>
	</div>
</div>
