<script>
	const reqBody = {
		nameObat: '',
		expired: '',
		stock: '',
		minStock: ''
	};

	const reqBodyupdate = {
		idObat: '',
		nameObat: '',
		expired: '',
		minStock: '',
		stock: '',

	};

	const handleUpdateObat = async () => {
		fetch(`http://localhost:8080/api/obat`, {
			method: 'PATCH',
			body: JSON.stringify(reqBodyupdate),
			headers: {
				'Content-type': 'application/json',
				'Access-Control-Allow-Origin': '*',
				'Access-Control-Allow-Methods': 'GET, POST, PATCH'
			}
		})
		.then((res) => res.json())
			.then((data) => {
				console.log(data);
			})
			.catch((err) => console.log(err));
	}

	const handleAddObat = async () => {
		// console.log(reqBody.expired)
		fetch(`http://localhost:8080/api/obat`, {
			method: 'POST',
			body: JSON.stringify(reqBody),
			headers: {
				'Content-type': 'application/json',
				'Access-Control-Allow-Origin': '*',
				'Access-Control-Allow-Methods': 'GET, POST'
			}
		})
			.then((res) => res.json())
			.then((data) => {
				console.log(data);
			})
			.catch((err) => console.log(err));
	};
</script>

<div class="container bg-transparent mt-4 rounded-md">
	<div class="flex justify-around">
		<div class="add">
			<div class="card w-96 bg-base-100 shadow-xl">
				<div class="card-body">
					<h2 class="card-title">Menambah Obat</h2>
					<form on:submit|preventDefault={handleAddObat}>
						<input
							type="text"
							placeholder="Nama Obat"
							name="name"
							class="input input-bordered w-full max-w-xs"
							bind:value={reqBody.nameObat}
						/>
						<label class="form-control w-full max-w-xs mt-2">
							<div class="label">
								<span class="label-text">Kadaluwarsa</span>
							</div>
							<input type="date" name="expired" bind:value={reqBody.expired} class="input input-bordered w-full max-w-xs" />
						</label>
						<input
							type="number"
							min="0"
							placeholder="Min Stok"
							name="minStock"
							class="input input-bordered w-full max-w-xs mt-2"
							bind:value={reqBody.minStock}
						/>
						<input
							type="number"
							min="0"
							placeholder="Stok Awal Bulan"
							name="stock"
							class="input input-bordered w-full max-w-xs mt-2"
							bind:value={reqBody.stock}
						/>

						<div class="card-actions justify-end mt-2">
							<button type="submit" class="btn btn-accent text-white">Simpan</button>
						</div>
					</form>
				</div>
			</div>
		</div>
		<div class="edit">
			<div class="card w-96 bg-base-100 shadow-xl">
				<div class="card-body">
					<h2 class="card-title">Mengubah Obat</h2>
					<form on:submit|preventDefault={handleUpdateObat}>
						<input
							type="text"
							name="idObat"
							placeholder="ID Obat"
							class="input input-bordered w-full h-12"
							bind:value={reqBodyupdate.idObat}
						/>
						<input
							type="text"
							placeholder="Nama Obat"
							name="nameObat"
							class="input input-bordered w-full h-12 mt-2"
							bind:value={reqBodyupdate.nameObat}
						/>
						<label class="form-control w-full max-w-xs mt-2">
							<div class="label">
								<span class="label-text">Kadaluwarsa</span>
							</div>
							<input type="date" bind:value={reqBodyupdate.expired} name="expired" class="input input-bordered w-full max-w-xs" />
						</label>
						<input
							type="number"
							min="0"
							placeholder="Min Stok"
							name="minStock"
							class="input input-bordered w-full max-w-xs mt-2"
							bind:value={reqBodyupdate.minStock}
						/>
						<input
							type="number"
							min="0"
							placeholder="Stok Awal Bulan"
							name="stock"
							class="input input-bordered w-full max-w-xs mt-2"
							bind:value={reqBodyupdate.stock}
						/>
						<div class="card-actions justify-end mt-2">
							<button class="btn btn-accent text-white">Simpan</button>
						</div>
					</form>
				</div>
			</div>
		</div>
	</div>
</div>
