<script>
	import '../../../../app.css';
	import { onMount } from 'svelte';

	/**
	 * @type {any}
	 */
	var response;

	onMount(() => {
		const url = new URL(window.location.href);
		const rm = url.searchParams.get('rm');
		const humberger = document.querySelector('#humberger');
		const navMenu = document.querySelector('#nav-menu');

		humberger?.addEventListener('click', function () {
			humberger.classList.toggle('humb-active');
			navMenu?.classList.toggle('hidden');
		});

		fetch(`http://localhost:8080/api/rm/${rm}`, {
			method: 'GET',
			headers: {
				'Content-type': 'application/json',
				'Access-Control-Allow-Origin': '*',
				'Access-Control-Allow-Methods': 'GET, POST'
			}
		})
			.then((res) => res.json())
			.then((data) => {
				response = data.data;
				console.log(data);
			})
			.catch((err) => console.log(err));
	});

	const backHandle = async () => {
		window.history.back();
	};
</script>

<header class="fixed top-0 left-0 w-full flex items-center justify-center z-10 shadow-md bg-white">
	<div class="container">
		<div class="flex items-center justify-between relative">
			<div class="px-4">
				<img src="../../Logo_Klinik.png" alt="unusa" class="w-16 py-6 block" />
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
							<button
								on:click={backHandle}
								class="bg-red-600 p-3 btn rounded-md hover:text-black text-base text-white py-2 mx-8 cursor-pointer flex lg:font-semibold"
								id="Log Out"
							>
								Kembali
							</button>
						</li>
					</ul>
				</nav>
			</div>
		</div>
	</div>
</header>

<section class="mt-36">
	<div class="container m-auto">
		<div class="overflow-x-auto">
			<table class="table">
				<!-- head -->
				<thead>
					<tr>
						<th>#</th>
						<th>Tanggal</th>
						<th>Anamnesa</th>
						<th>Diagnosa</th>
						<th>Terapi</th>
						<th>Jumlah Obat</th>
					</tr>
				</thead>
				{#if response}
					{#each response as res, i}
						<tbody>
							<tr class="hover">
								<td>{++i}</td>
								<td>{res.checkin}</td>
								<td>{res.pemeriksaan}</td>
								<td>{res.anamnesa}</td>
								<td>{res.diagnosis}</td>
								<td>
									<li>{res.therapy}</li>
									<li>{res.therapy2 != null ? res.therapy2 : ''}</li>
									<li>{res.therapy3 != null ? res.therapy3 : ''}</li>
									<li>{res.therapy4 != null ? res.therapy4 : ''}</li>
								</td>
								<td>
									<li>{res.jumlahObat}</li>
									<li>{res.jumlahObat2 != null ? res.jumlahObat2 : ''}</li>
									<li>{res.jumlahObat3 != null ? res.jumlahObat3 : ''}</li>
									<li>{res.jumlahObat4 != null ? res.jumlahObat4 : ''}</li>
								</td>
							</tr>
						</tbody>
					{/each}
				{/if}
			</table>
		</div>
	</div>
</section>
