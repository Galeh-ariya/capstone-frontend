<script>
	import './rm.css';
	import '../../app.css';
	import { onMount } from 'svelte';
	import { setContext } from 'svelte';

	var response = {
		name: '',
		email: '',
		instansi: '',
		gender: '',
		noRm: '',
		tempat_lahir: '',
		tanggal_lahir: ''
	};

	onMount(() => {
		const url = new URL(window.location.href);
		const message = url.searchParams.get('message');
		const humberger = document.querySelector('#humberger');
		const navMenu = document.querySelector('#nav-menu');

		humberger?.addEventListener('click', function () {
			humberger.classList.toggle('humb-active');
			navMenu?.classList.toggle('hidden');
		});

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
				// console.log(data);
			})
			.catch((err) => console.log(err));
	});

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

	/**
	 * @type {any}
	 */
	let dataRekam;

	const getDatahandler = async () => {
		fetch(`http://localhost:8080/api/rm/${response.noRm}`, {
			method: 'GET',
			headers: {
				'Content-type': 'application/json',
				'Access-Control-Allow-Origin': '*',
				'Access-Control-Allow-Methods': 'GET, POST'
			}
		})
			.then((res) => res.json())
			.then((data) => {
				dataRekam = data.data;
				console.log(data);
			})
			.catch((err) => console.log(err));
	};
</script>

<header class="fixed top-0 left-0 w-full flex items-center justify-center z-10 shadow-md bg-white">
	<div class="container">
		<div class="flex items-center justify-between relative">
			<div class="px-4">
				<img src="unusa.png" alt="unusa" class="w-16 py-6 block" />
			</div>
			<div class="flex items-center px-4">
				<button
					id="humberger"
					name="humberger"
					type="button"
					class="block absolute right-4 lg:hidden"
				>
					<span class="hum-line transition duration-300 ease-in-out origin-top-left"></span>
					<span class="hum-line transition duration-300 ease-in-out"></span>
					<span class="hum-line transition duration-300 ease-in-out origin-bottom-left"></span>
				</button>

				<nav
					id="nav-menu"
					class="hidden absolute py-5 bg-white shadow-md rounded-md max-w-[250px] w-full right-4 top-full lg:block lg:static lg:max-w-full lg:shadow-none lg:rounded-none lg:right-0"
				>
					<ul class="block md:flex">
						<li class="group">
							<a
								href="/"
								class="text-base text-black py-2 mx-8 hover:text-[#66D3D6] cursor-pointer flex lg:font-semibold"
								id="home"
							>
								Home
							</a>
						</li>

						<li>
							<a
								href="/login/coba"
								class="text-base py-2 mx-8 text-[#66D3D6] cursor-pointer flex font-semibold"
								><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
									><path
										fill="currentColor"
										d="M16 11V8h-3V6h3V3h2v3h3v2h-3v3zm3.95 10q-3.125 0-6.175-1.362t-5.55-3.863q-2.5-2.5-3.862-5.55T3 4.05q0-.45.3-.75t.75-.3H8.1q.35 0 .625.238t.325.562l.65 3.5q.05.4-.025.675T9.4 8.45L6.975 10.9q.5.925 1.187 1.787t1.513 1.663q.775.775 1.625 1.438T13.1 17l2.35-2.35q.225-.225.588-.337t.712-.063l3.45.7q.35.1.575.363T21 15.9v4.05q0 .45-.3.75t-.75.3"
									/></svg
								> +62 838 333 578 66</a
							>
						</li>
						<li class="group">
							<button
								on:click={logoutHandle}
								class="bg-red-600 p-3 btn rounded-md hover:text-black text-base text-white py-2 mx-8 cursor-pointer flex lg:font-semibold"
								id="Log Out"
							>
								Log Out
							</button>
						</li>
					</ul>
				</nav>
			</div>
		</div>
	</div>
</header>

<section class="bg-[url('bg-hero.png')] mt-24 w-full h-[25rem] md:h-80 pt-20 p-10">
	<h1 class="text-center font-bold text-white text-3xl mb-8">Data Pasien</h1>

	<form>
		<div class="text-white font-semibold text-center flex justify-around">
			<div class="mx-4">
				<div>
					<label for="">Nama: </label>
					<input type="text" class="input input-bordered input-sm my-2 w-40 md:w-auto" value="{response.name}" disabled />
				</div>
				<div>
					<label for="">Email: </label>
					<input type="text" class="input input-bordered input-sm my-2 w-40 md:w-auto" disabled value="{response.email}" />
				</div>
				<div>
					<label for="">Instansi: </label>
					<input type="text" class="input input-bordered input-sm my-2 w-40 md:w-auto" disabled value="{response.instansi}" />
				</div>
			</div>
			<div >
				<div>
					<label for="">TTL: </label>
					<input type="text" class="input input-bordered input-sm my-2 w-40 md:w-auto" value="{response.tempat_lahir + ', ' + response.tanggal_lahir}" disabled />
				</div>
				<div>
					<label for="">No Rm: </label>
					<input type="text" class="input input-bordered input-sm my-2 w-40 md:w-auto" disabled value="{response.noRm}" />
				</div>
				<div>
					<label for="">Gender: </label>
					<input type="text" class="input input-bordered input-sm my-2 w-40 md:w-auto" disabled value="{response.gender}" />
				</div>
			</div>
		</div>
	</form>
</section>

<section class="flex justify-center items-center mt-11">
	<div class="container p-5">
		<button on:click={getDatahandler} class="btn btn-accent text-white">Tampilkan Data</button>
		{#if dataRekam}
			{#each dataRekam as rekam}
				<div class="collapse collapse-arrow bg-base-200">
					<input type="radio" name="my-accordion-2" />
					<div class="collapse-title text-xl font-medium">
						<span class="bg-red-600 p-1 rounded-md text-white text-[10px]">{rekam.checkin}</span>
						{rekam.diagnosis}
					</div>
					<div class="collapse-content">
						<div class="overflow-x-auto">
							<table class="table">
								<!-- head -->
								<thead>
									<tr class="bg-[#66D3D6] text-bold text-white">
										<th>ANAMESA</th>
										<th>DIAGNOSA</th>
										<th>TERAPI</th>
										<th>KETERANGAN</th>
									</tr>
								</thead>
								<tbody>
									<!-- row 1 -->
									<tr>
										<th>{rekam.anamnesa}</th>
										<td>{rekam.diagnosis}</td>
										<td>{rekam.therapy}</td>
										<td>{rekam.jumlahObat}</td>
									</tr>
								</tbody>
							</table>
						</div>
					</div>
				</div>
			{/each}
		{/if}
	</div>
</section>
