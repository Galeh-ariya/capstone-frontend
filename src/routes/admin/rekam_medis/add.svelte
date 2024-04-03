<script>
// @ts-nocheck


import { onMount } from 'svelte';

	/**
	 * @type {HTMLElement | null}
	 */
	let failed;
	/**
	 * @type {HTMLElement | null}
	 */
	let success;

	/**
	 * @type {any[]}
	 */
	let dataNameObat;

	onMount(() => {
		failed = document.getElementById(`failed`);
		success = document.getElementById(`success`);

		fetch(`http://localhost:8080/api/nameObat`, {
			method: 'GET', 
			headers: {
				'Content-type': 'application/json',
				'Access-Control-Allow-Origin': '*',
				'Access-Control-Allow-Methods': 'GET, POST, DELETE'
			}
		})
		.then((res) => res.json())
		.then((data) => {
			console.log(data.data)
			dataNameObat = data.data
		})
		.catch((err) => {
				console.log(err);
			});
	});


	let reqBody = {
		name: '',
		email: '',
		gender: '',
		tempat_lahir: '',
		birthDate: '',
		instansi: '',
		category: '',
		anamnesa: '',
		pemeriksaan: '',
		diagnosis: '',
		therapy: '',
		therapy2: '',
		therapy3: '',
		therapy4: '',
		totalObat: '',
		totalObat2: '',
		totalObat3: '',
		totalObat4: ''
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
				if(data.data != null) {
					// @ts-ignore
					success.showModal();
				} else {
					// @ts-ignore
					failed.showModal();
				}
				console.log(data);
			})
			.catch((err) => console.log(err));
	};

	/**
	 * @type {any[]}
	 */
	 let filteredData = [];
  	

	  let showList = false;
	  let showList2 = false;
	  let showList3 = false;
	  let showList4 = false;

	/**
	 * @param {{ target: { value: string; }; }} event
	 */
	function onInput1(event) {
		reqBody.therapy = event.target.value;
		filteredData = dataNameObat.filter((item) => item.toLowerCase().includes(reqBody.therapy.toLowerCase()));
		showList = true;
  	}

	/**
	 * @param {{ target: { value: string; }; }} event
	 */
	 function onInput2(event) {
		reqBody.therapy2 = event.target.value;
		filteredData = dataNameObat.filter((item) => item.toLowerCase().includes(reqBody.therapy2.toLowerCase()));
		showList2 = true;
  	}
	
	/**
	 * @param {{ target: { value: string; }; }} event
	 */
	function onInput3(event) {
		reqBody.therapy3 = event.target.value;
		filteredData = dataNameObat.filter((item) => item.toLowerCase().includes(reqBody.therapy3.toLowerCase()));
		showList3 = true;
  	}
	
	/**
	 * @param {{ target: { value: string; }; }} event
	 */
	function onInput4(event) {
		reqBody.therapy4 = event.target.value;
		filteredData = dataNameObat.filter((item) => item.toLowerCase().includes(reqBody.therapy4.toLowerCase()));
		showList4 = true;
  	}

</script>

<dialog id="success" class="modal">
	<div class="modal-box">
		<h3 class="font-bold text-lg text-green-500">Berhasil!</h3>
		<p class="py-4">Data berhasil dimasukkan!</p>
		<svg
			xmlns="http://www.w3.org/2000/svg"
			class="w-32 h-32 animate-bounce text-green-500 mt-10 mx-auto"
			viewBox="0 0 512 512"
			><path
				fill="currentColor"
				d="M256 48a208 208 0 1 1 0 416a208 208 0 1 1 0-416m0 464a256 256 0 1 0 0-512a256 256 0 1 0 0 512m113-303c9.4-9.4 9.4-24.6 0-33.9s-24.6-9.4-33.9 0l-111 111l-47-47c-9.4-9.4-24.6-9.4-33.9 0s-9.4 24.6 0 33.9l64 64c9.4 9.4 24.6 9.4 33.9 0z"
			/></svg
		>
		<div class="modal-action">
			<form method="dialog">
				<!-- if there is a button in form, it will close the modal -->
				<button class="btn">Close</button>
			</form>
		</div>
	</div>
</dialog>

<dialog id="failed" class="modal">
	<div class="modal-box">
		<h3 class="font-bold text-lg text-red-600">Gagal!</h3>
		<p class="py-4">data yang anda masukkan tidak valid!</p>
		<svg
			xmlns="http://www.w3.org/2000/svg"
			class="w-32 h-32 animate-bounce text-red-600 mt-10 mx-auto"
			viewBox="0 0 512 512"
			><path
				fill="currentColor"
				d="M256 48a208 208 0 1 1 0 416a208 208 0 1 1 0-416m0 464a256 256 0 1 0 0-512a256 256 0 1 0 0 512m-81-337c-9.4 9.4-9.4 24.6 0 33.9l47 47l-47 47c-9.4 9.4-9.4 24.6 0 33.9s24.6 9.4 33.9 0l47-47l47 47c9.4 9.4 24.6 9.4 33.9 0s9.4-24.6 0-33.9l-47-47l47-47c9.4-9.4 9.4-24.6 0-33.9s-24.6-9.4-33.9 0l-47 47l-47-47c-9.4-9.4-24.6-9.4-33.9 0"
			/></svg
		>
		<div class="modal-action">
			<form method="dialog">
				<!-- if there is a button in form, it will close the modal -->
				<button class="btn">Close</button>
			</form>
		</div>
	</div>
</dialog>

<!-- Main Content --><!-- Main Content -->
<div class="p-10 ml-60">
	<!-- Your main content here -->
	<h1 class="text-xl font-bold">Menambah Pasien</h1>

	<section class="w-full h-full pt-20 p-10 flex justify-center items-center">
		<div class="card w-full bg-base-100 shadow-xl">
			<div class="card-body font-semibold mx-4">
				<form on:submit|preventDefault={addNewUserHandler}>
					<div class="flex relative space-x-9">
						<div class="">
							<input
								type="text"
								placeholder="Nama"
								name="name"
								class="input input-bordered w-full max-w-xs my-3"
								bind:value={reqBody.name}
							/>
							<input
								type="text"
								placeholder="E-mail"
								name="email"
								class="input input-bordered w-full max-w-xs my-3"
								bind:value={reqBody.email}
							/>
							<div class="my-3">
								<label for="jk">Jenis Kelamin</label> <br />
								<select
									class="select select-bordered w-full max-w-xs"
									name="gender"
									bind:value={reqBody.gender}
									id="jk"
								>
									<option selected value="laki-laki">Laki-laki</option>
									<option value="perempuan">Perempuan</option>
								</select>
							</div>

							<input
								type="text"
								name="tempat_lahir"
								placeholder="Tempat Lahir"
								class="input border-[#cdc9c9] mt-2 w-28 textarea-xs my-3"
								bind:value={reqBody.tempat_lahir}
							/>
							<input
								type="date"
								name="tanggal_lahir"
								placeholder="tanggal Lahir"
								class="input border-[#cdc9c9] mt-2 w-40"
								bind:value={reqBody.birthDate}
							/>
							<br />
							<input
								type="text"
								placeholder="Instansi"
								name="instansi"
								class="input input-bordered w-full max-w-xs mt-2 my-3"
								bind:value={reqBody.instansi}
							/>

							<div class="my-3">
								<label for="kategori">Kategori</label> <br />
								<select
									class="select select-bordered w-full max-w-xs mt-2"
									name="kategori"
									bind:value={reqBody.category}
									id="kategori"
								>
									<option selected value="M">Mahasiswa</option>
									<option value="K">Karyawan</option>
								</select>
							</div>
						</div>

						<hr class="mt-4" />

						<div>
							<input
								type="text"
								placeholder="Anamnesa"
								name="anamnesa"
								class="input input-bordered w-full max-w-xs mt-2"
								bind:value={reqBody.anamnesa}
							/> <br>
							<input
								type="text"
								placeholder="Pemeriksaan"
								name="pemeriksaan"
								class="input input-bordered w-full max-w-xs mt-2"
								bind:value={reqBody.pemeriksaan}
							/>
							<input
								type="text"
								placeholder="Diagnosa"
								name="diagnosis"
								class="input input-bordered w-full max-w-xs mt-2"
								bind:value={reqBody.diagnosis}
							/>

							<div class="flex">
								<input
									type="text"
									placeholder="Terapi 1"
									name="terapi1"
									class="input input-bordered w-full max-w-xs mt-2"
									bind:value={reqBody.therapy}
									on:input={onInput1}
								/>
								{#if showList}
									<ul class="absolute bg-white border border-gray-300 list-none mt-16 w-80 rounded-md p-2 shadow-md">
										{#each filteredData as item}
											<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
											<!-- svelte-ignore a11y-click-events-have-key-events -->
											<li class="hover:bg-gray-100 cursor-pointer" on:click={() => { reqBody.therapy = item; showList = false; }}>{item}</li>
										{/each}
									</ul>
								{/if}

								<input
									type="number"
									min="0"
									placeholder="Jumlah"
									name="jumlah1"
									class="input input-bordered w-28 mt-2 mx-2"
									bind:value={reqBody.totalObat}
								/>
							</div>

							<div class="flex">
								<input
									type="text"
									placeholder="Terapi 2"
									name="terapi2"
									class="input input-bordered w-full max-w-xs mt-2"
									bind:value={reqBody.therapy2}
									on:input={onInput2}
								/>
								{#if showList2}
									<ul class="absolute bg-white border border-gray-300 list-none mt-16 w-80 rounded-md p-2 shadow-md">
										{#each filteredData as item}
											<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
											<!-- svelte-ignore a11y-click-events-have-key-events -->
											<li class="hover:bg-gray-100 cursor-pointer" on:click={() => { reqBody.therapy2 = item; showList2 = false; }}>{item}</li>
										{/each}
									</ul>
								{/if}

								<input
									type="number"
									min="0"
									placeholder="Jumlah"
									name="jumlah2"
									class="input input-bordered w-28 mt-2 mx-2"
									bind:value={reqBody.totalObat2}
								/>
							</div>

							<div class="flex">
								<input
									type="text"
									placeholder="Terapi 3"
									name="terapi3"
									class="input input-bordered w-full max-w-xs mt-2"
									bind:value={reqBody.therapy3}
									on:input={onInput3}
								/>
								{#if showList3}
									<ul class="absolute bg-white border border-gray-300 list-none mt-16 w-80 rounded-md p-2 shadow-md">
										{#each filteredData as item}
											<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
											<!-- svelte-ignore a11y-click-events-have-key-events -->
											<li class="hover:bg-gray-100 cursor-pointer" on:click={() => { reqBody.therapy3 = item; showList3 = false; }}>{item}</li>
										{/each}
									</ul>
								{/if}

								<input
									type="number"
									min="0"
									placeholder="Jumlah"
									name="jumlah3"
									class="input input-bordered w-28 mt-2 mx-2"
									bind:value={reqBody.totalObat3}
								/>
							</div>

							<div class="flex">
								<input
									type="text"
									placeholder="Terapi 4"
									name="terapi4"
									class="input input-bordered w-full max-w-xs mt-2"
									bind:value={reqBody.therapy4}
									on:input={onInput4}
								/>
								{#if showList4}
									<ul class="absolute bg-white border border-gray-300 list-none mt-16 w-80 rounded-md p-2 shadow-md">
										{#each filteredData as item}
											<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
											<!-- svelte-ignore a11y-click-events-have-key-events -->
											<li class="hover:bg-gray-100 cursor-pointer" on:click={() => { reqBody.therapy4 = item; showList4 = false; }}>{item}</li>
										{/each}
									</ul>
								{/if}

								<input
									type="number"
									min="0"
									placeholder="Jumlah"
									name="jumlah4"
									class="input input-bordered w-28 mt-2 mx-2"
									bind:value={reqBody.totalObat4}
								/>
							</div>

							<!-- <input
								type="number"
								min="0"
								placeholder="Jumlah Obat"
								name="total"
								class="input input-bordered w-full max-w-xs mt-2"
								bind:value={reqBody.totalObat}
							/> -->
							<div class="card-actions justify-end mt-2">
								<button type="submit" name="submit" class="btn btn-accent text-white w-full">Simpan</button>
							</div>
						</div>
					</div>
				</form>
			</div>
		</div>
	</section>
</div>
