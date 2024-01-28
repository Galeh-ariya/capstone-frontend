<script>
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

	onMount(() => {
		failed = document.getElementById(`failed`);
		success = document.getElementById(`success`);
	});

	const reqBody = {
		anamnesa: '',
		diagnosis: '',
		therapy: '',
		jumlahObat: ''
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
				if (data.data !=  null) {
					// @ts-ignore
					success.showModal();
					reqBody.anamnesa = ''
					reqBody.diagnosis = ''
					reqBody.therapy = ''
					reqBody.jumlahObat = ''
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

<section class=" w-full h-[510px] pt-20 p-10 flex justify-center items-center">
	<div class="card w-96 bg-base-100 shadow-xl">
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
					placeholder="Diagnosa"
					class="input input-bordered w-full max-w-xs text-[#6C757D] mt-2"
					name="diagnosis"
					bind:value={reqBody.diagnosis}
				/>
				<input
					type="text"
					placeholder="Terapi"
					name="therapy"
					class="input input-bordered w-full max-w-xs text-[#6C757D] mt-2"
					bind:value={reqBody.therapy}
				/>
				<input
					type="number"
					min="0"
					placeholder="Jumlah Obat"
					name="jumlahObat"
					class="input input-bordered w-full max-w-xs text-[#6C757D] mt-2"
					bind:value={reqBody.jumlahObat}
				/>
				<div class="card-actions justify-center mt-4">
					<button class="btn bg-[#66D3D6] text-white w-full font-semibold">Tambah</button>
					<!-- <button on:click={backHandler} class="btn bg-red-600 text-white w-full font-semibold"
						>Kembali</button
					> -->
				</div>
			</form>
		</div>
	</div>
</section>
