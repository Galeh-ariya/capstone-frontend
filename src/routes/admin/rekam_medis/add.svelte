<script>

	let reqBody = {
		name: '',
		email: '',
		gender: '',
		tempat_lahir: '',
		birthDate: '',
		instansi: '',
		category: '',
		anamnesa: '',
		diagnosis: '',
		therapy: '',
		totalObat: ''
	};
	const addNewUserHandler = async () => {
		console.log(reqBody.birthDate);
		fetch(`http://localhost:8080/api/users`, {
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

<!-- Main Content --><!-- Main Content -->
<div class="p-10">
	<!-- Your main content here -->
	<h1 class="text-xl font-bold">Menambah Pasien</h1>

	<section class="w-full h-full pt-20 p-10 flex justify-center items-center">
		<div class="card w-full bg-base-100 shadow-xl">
			<div class="card-body font-semibold mx-4">
				<form on:submit={addNewUserHandler}>
					<div class="flex relative">
						<div>
							<input
								type="text"
								placeholder="Nama"
								name="name"
								class="input input-bordered w-full max-w-xs"
								bind:value={reqBody.name}
							/>
							<input
								type="text"
								placeholder="E-mail"
								name="email"
								class="input input-bordered w-full max-w-xs"
								bind:value={reqBody.email}
							/>
							<select
								class="select select-bordered w-full max-w-xs mt-2"
								name="gender"
								bind:value={reqBody.gender}
							>
								<option disabled selected>Jenis Kelamin</option>
								<option value="laki-laki">Laki-laki</option>
								<option value="perempuan">Perempuan</option>
							</select>
							<input
								type="text"
								name="tempat_lahir"
								placeholder="Tempat Lahir"
								class="input border-[#cdc9c9] mt-2 w-28 textarea-xs"
								bind:value={reqBody.tempat_lahir}
							/>
							<input
								type="date"
								name="tanggal_lahir"
								placeholder="tanggal Lahir"
								class="input border-[#cdc9c9] mt-2 w-28"
								bind:value={reqBody.birthDate}
							/>
							<input
								type="text"
								placeholder="Instansi"
								name="instansi"
								class="input input-bordered w-full max-w-xs mt-2"
								bind:value={reqBody.instansi}
							/>
							<select
								class="select select-bordered w-full max-w-xs mt-2"
								name="kategori"
								bind:value={reqBody.category}
							>
								<option disabled selected>Kategori</option>
								<option value="M">Mahasiswa</option>
								<option value="K">Karyawan</option>
							</select>
						</div>

						<hr class="mt-4" />

						<div>
							<input
								type="text"
								placeholder="Anamnesa"
								name="anamnesa"
								class="input input-bordered w-full max-w-xs mt-2"
								bind:value={reqBody.anamnesa}
							/>
							<input
								type="text"
								placeholder="Diagnosa"
								name="diagnosis"
								class="input input-bordered w-full max-w-xs mt-2"
								bind:value={reqBody.diagnosis}
							/>
							<input
								type="text"
								placeholder="Terapi"
								name="terapi"
								class="input input-bordered w-full max-w-xs mt-2"
								bind:value={reqBody.therapy}
							/>
							<input
								type="number"
								min="0"
								placeholder="Jumlah Obat"
								name="total"
								class="input input-bordered w-full max-w-xs mt-2"
								bind:value={reqBody.totalObat}
							/>
							<div class="card-actions justify-end mt-2">
								<button class="btn btn-accent text-white">Simpan</button>
							</div>
						</div>
					</div>
				</form>
			</div>
		</div>
	</section>
</div>
