<script>
	import { onMount } from 'svelte';

	/**
	 * @type {any}
	 */
	let dataObat;

	onMount(() => {
		fetch('http://localhost:8080/api/obat', {
			method: 'GET',
			headers: {
				'Content-type': 'application/json',
				'Access-Control-Allow-Origin': '*',
				'Access-Control-Allow-Methods': 'GET, POST, DELETE'
			}
		})
			.then((res) => res.json())
			.then((data) => {
				dataObat = data.data;
				console.log(data);
			})
			.catch((err) => console.log(err));
	});

    
</script>

<div class="container bg-white mt-4 rounded-md">
	<div class="overflow-x-auto">
		<table class="table">
			<!-- head -->
			<thead>
				<tr>
					<th>No</th>
					<th>ID obat</th>
					<th>Nama Obat</th>
					<th>Exp</th>
					<th>Min Stok</th>
					<th>Stok Awal Bulan</th>
					<th>Jumlah Terpakai</th>
					<th>Stok Akhir Bulan</th>
                    <th>Status</th>
				</tr>
			</thead>
			{#if dataObat}
				{#each dataObat as obat, i}
                <tbody>
                    <tr>
                        <th>{++i}</th>
                        <th>{obat.idObat}</th>
                        <td>{obat.nameObat}</td>
                        <td>{obat.expired}</td>
                        <td>{obat.minStock}</td>
                        <td>{obat.stock}</td>
                        <td>{obat.usedTotal}</td>
                        <td>{obat.stock - obat.usedTotal}</td>
                        <td>
                            {#if obat.stock > obat.minStock }
                                <div class="w-10 h-4 bg-green-600"></div>
                            {:else} 
                                <div class="w-10 h-4 bg-red-600"></div>
                            {/if}
                            
                        </td>
                    </tr>
                </tbody>
                {/each}
			{/if}
			
		</table>
	</div>
</div>
