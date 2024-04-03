<script>
// @ts-nocheck

	import '../../../../app.css';
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
	let dataNameObat = [];

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

	const reqBody = {
		anamnesa: '',
		pemeriksaan: '',
		diagnosis: '',
		therapy: '',
		therapy2: '',
		therapy3: '',
		therapy4: '',
		jumlahObat: '',
		jumlahObat2: '',
		jumlahObat3: '',
		jumlahObat4: ''
	};

	const addRekamHandler = async () => {
		const url = new URL(window.location.href);
		const rm = url.searchParams.get('rm');

		fetch(`http://localhost:8080/api/rm/${rm}`, {
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
				if (data.data != null) {
					// @ts-ignore
					success.showModal();
					// reqBody.anamnesa = '';
					// reqBody.diagnosis = '';
					// reqBody.therapy = '';
					// reqBody.jumlahObat = '';
				} else {
					// @ts-ignore
					failed.showModal();
				}
				console.log(data);
			})
			.catch((err) => {
				// @ts-ignore
				failed.showModal();
				console.log(err);
			});
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

<section class=" w-full h-[510px] pt-20 p-10 flex justify-center items-center mt-8">
	<div class="card w-[610px] bg-base-100 shadow-xl">
		<div class="card-body font-semibold mx-4">
			<h2 class="card-title justify-center mb-6 text-[#6C757D]">Tambah Data</h2>
			<form on:submit|preventDefault={addRekamHandler}>
				<input
					type="text"
					placeholder="Anamesa"
					class="input input-bordered w-full max-w-xs text-[#6C757D]"
					name="anamnesa"
					bind:value={reqBody.anamnesa}
				/>
				<input
					type="text"
					placeholder="Pemeriksaan"
					class="input input-bordered w-full max-w-xs text-[#6C757D] mt-2"
					name="pemeriksaan"
					bind:value={reqBody.pemeriksaan}
				/>
				<input
					type="text"
					placeholder="Diagnosa"
					class="input input-bordered w-full max-w-xs text-[#6C757D] mt-2"
					name="diagnosis"
					bind:value={reqBody.diagnosis}
				/>

				<!-- <div class="mt-10">
					<input type="text" bind:value={searchText} on:input={onInput} class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-1 focus:ring-blue-500" />
					{#if showList}
						<ul class="absolute top-full left-0 w-full bg-white border border-gray-300 list-none p-0 m-0 shadow-md">
						{#each filteredData as item} -->
							<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
							<!-- svelte-ignore a11y-click-events-have-key-events -->
							<!-- <li class="px-3 py-2 hover:bg-gray-100 cursor-pointer" on:click={() => { searchText = item; showList = false; }}>{item}</li>
						{/each}
						</ul>
					{/if}
				</div> -->

				<!-- memperbaiki inputan menjadi search auto complete dengan cara mengganti search text ke reqbody satu persatu -->
				<div class="flex space-x-2">
					<div class="w-80">
						<input
						type="text"
						id="t1"
						placeholder="Terapi 1"
						name="therapy"
						class="input input-bordered w-full max-w-xs text-[#6C757D] mt-2"
						bind:value={reqBody.therapy}
						on:input={onInput1} />
						{#if showList}
							<ul class="absolute bg-white border border-gray-300 list-none mt-3 w-80 rounded-md p-2 shadow-md">
								{#each filteredData as item}
									<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
									<!-- svelte-ignore a11y-click-events-have-key-events -->
									<li class="hover:bg-gray-100 cursor-pointer" on:click={() => { reqBody.therapy = item; showList = false; }}>{item}</li>
								{/each}
							</ul>
						{/if}
					</div>

					<input
						type="number"
						min="0"
						placeholder="Jumlah"
						name="jumlahObat"
						class="input input-bordered w-28 max-w-xs text-[#6C757D] mt-2"
						bind:value={reqBody.jumlahObat}
					/>
				</div>

				<div class="flex space-x-2">
					<div class="w-80">
						<input
						type="text"
						id="t2"
						placeholder="Terapi 2"
						name="therapy2"
						class="input input-bordered w-full max-w-xs text-[#6C757D] mt-2"
						bind:value={reqBody.therapy2}
						on:input={onInput2} />
						{#if showList2}
							<ul class="absolute bg-white border border-gray-300 list-none mt-3 w-80 rounded-md p-2 shadow-md">
								{#each filteredData as item}
									<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
									<!-- svelte-ignore a11y-click-events-have-key-events -->
									<li class="hover:bg-gray-100 cursor-pointer" on:click={() => { reqBody.therapy2 = item; showList2 = false; }}>{item}</li>
								{/each}
							</ul>
						{/if}
					</div>

					<input
						type="number"
						min="0"
						placeholder="Jumlah"
						name="jumlahObat2"
						class="input input-bordered w-28 max-w-xs text-[#6C757D] mt-2"
						bind:value={reqBody.jumlahObat2}
					/>
				</div>
				
				<div class="flex space-x-2">
					<div class="w-80">
						<input
						type="text"
						id="t3"
						placeholder="Terapi 3"
						name="therapy3"
						class="input input-bordered w-full max-w-xs text-[#6C757D] mt-2"
						bind:value={reqBody.therapy3}
						on:input={onInput3} />
						{#if showList3}
							<ul class="absolute bg-white border border-gray-300 list-none mt-3 w-80 rounded-md p-2 shadow-md">
								{#each filteredData as item}
									<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
									<!-- svelte-ignore a11y-click-events-have-key-events -->
									<li class="hover:bg-gray-100 cursor-pointer" on:click={() => { reqBody.therapy3 = item; showList3 = false; }}>{item}</li>
								{/each}
							</ul>
						{/if}
					</div>

					<input
						type="number"
						min="0"
						placeholder="Jumlah"
						name="jumlahObat3"
						class="input input-bordered w-28 max-w-xs text-[#6C757D] mt-2"
						bind:value={reqBody.jumlahObat3}
					/>
				</div>
				
				<div class="flex space-x-2">
					<div class="w-80">
						<input
						type="text"
						id="t4"
						placeholder="Terapi 4"
						name="therapy4"
						class="input input-bordered w-full max-w-xs text-[#6C757D] mt-2"
						bind:value={reqBody.therapy4}
						on:input={onInput4} />
						{#if showList4}
							<ul class="absolute bg-white border border-gray-300 list-none mt-3 w-80 rounded-md p-2 shadow-md">
								{#each filteredData as item}
									<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
									<!-- svelte-ignore a11y-click-events-have-key-events -->
									<li class="hover:bg-gray-100 cursor-pointer" on:click={() => { reqBody.therapy4 = item; showList4 = false; }}>{item}</li>
								{/each}
							</ul>
						{/if}
					</div>

					<input
						type="number"
						min="0"
						placeholder="Jumlah"
						name="jumlahObat4"
						class="input input-bordered w-28 max-w-xs text-[#6C757D] mt-2"
						bind:value={reqBody.jumlahObat4}
					/>
				</div>

				<div class="card-actions justify-center mt-4">
					<!-- <button class="btn bg-red-600 text-white w-28 font-semibold">Kembali</button> -->
					<button class="btn bg-[#66D3D6] text-white w-28 font-semibold">Tambah</button>
				</div>
			</form>
		</div>
	</div>
</section>
