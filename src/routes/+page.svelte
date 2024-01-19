<script>
	import '../app.css';
	import { onMount } from 'svelte';
	

	onMount(() => {
		const humberger = document.querySelector('#humberger');
		const navMenu = document.querySelector('#nav-menu');

		const well = document.querySelector('#well');
		const come = document.querySelector('#come');
		const jadwal = document.querySelector('#jadwal');
		const home = document.querySelector('#home');

		humberger?.addEventListener('click', function () {
			humberger.classList.toggle('humb-active');
			navMenu?.classList.toggle('hidden');
		});

		jadwal?.addEventListener('click', function () {
			well?.classList.add('hidden');
			come?.classList.remove('hidden');
		});

		home?.addEventListener('click', function () {
			come?.classList.add('hidden');
			well?.classList.remove('hidden');
		});
	});
</script>

<!-- Navbar -->
<header
	class="absolute top-0 left-0 w-full flex items-center justify-center z-10 shadow-md bg-white"
>
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
							<p
								class="text-base text-black py-2 mx-8 hover:text-[#66D3D6] cursor-pointer flex lg:font-semibold"
								id="home"
							>
								Home
							</p>
						</li>
						<li class="group">
							<p
								class="text-base text-black py-2 mx-8 hover:text-[#66D3D6] cursor-pointer flex lg:font-semibold"
								id="jadwal"
							>
								Jadwal
							</p>
						</li>
						<li>
							<a
								href="https://unusa.ac.id"
								class="text-base py-2 mx-8 text-[#66D3D6] cursor-pointer flex font-semibold"
								><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
									><path
										fill="currentColor"
										d="M16 11V8h-3V6h3V3h2v3h3v2h-3v3zm3.95 10q-3.125 0-6.175-1.362t-5.55-3.863q-2.5-2.5-3.862-5.55T3 4.05q0-.45.3-.75t.75-.3H8.1q.35 0 .625.238t.325.562l.65 3.5q.05.4-.025.675T9.4 8.45L6.975 10.9q.5.925 1.187 1.787t1.513 1.663q.775.775 1.625 1.438T13.1 17l2.35-2.35q.225-.225.588-.337t.712-.063l3.45.7q.35.1.575.363T21 15.9v4.05q0 .45-.3.75t-.75.3"
									/></svg
								> +62 838 333 578 66</a
							>
						</li>
					</ul>
				</nav>
			</div>
		</div>
	</div>
</header>

<section class="bg-[url('bg-hero.png')] mt-24 w-full h-[510px] pt-20 p-10">
	<div class="container flex justify-around items-center">
		<div class="ml-10" id="well">
			<h1 class="text-5xl font-bold text-white mb-4">KLIKNIK <br /> PRATAMA UNUSA|</h1>
			<p class="text-white mb-4">
				Klinik pratama adalah salah satu klinik milik UNUSA yang berdiri sejak tahun 500 sebelum
				masehi
			</p>
			<div class="flex items-center">
				<a href="/login"><button class="btn bg-white text-[#66D3D6] hover:bg-white mr-3">Login</button></a>
				<button
					class="btn btn-outline border-white text-white hover:bg-white hover:text-[#66D3D6] hover:border-none"
					><svg
						class="text-white hover:text-[#66D3D6] w-8"
						xmlns="http://www.w3.org/2000/svg"
						viewBox="0 0 24 24"
						><g fill="none"
							><path
								d="M24 0v24H0V0zM12.593 23.258l-.011.002l-.071.035l-.02.004l-.014-.004l-.071-.035c-.01-.004-.019-.001-.024.005l-.004.01l-.017.428l.005.02l.01.013l.104.074l.015.004l.012-.004l.104-.074l.012-.016l.004-.017l-.017-.427c-.002-.01-.009-.017-.017-.018m.265-.113l-.013.002l-.185.093l-.01.01l-.003.011l.018.43l.005.012l.008.007l.201.093c.012.004.023 0 .029-.008l.004-.014l-.034-.614c-.003-.012-.01-.02-.02-.022m-.715.002a.023.023 0 0 0-.027.006l-.006.014l-.034.614c0 .012.007.02.017.024l.015-.002l.201-.093l.01-.008l.004-.011l.017-.43l-.003-.012l-.01-.01z"
							/><path
								fill="currentColor"
								d="M5 9a7 7 0 0 1 14 0v1.035c1.696.243 3 1.702 3 3.465v.25c0 1.775-1.531 3.331-3.332 3.248c-.74 2.12-2.622 3.549-4.653 3.911c-.47.172-1.026.091-1.515.091a1.5 1.5 0 0 1 0-3c.793 0 1.671-.115 2.207.609C16.003 17.992 17 16.689 17 15V9A5 5 0 0 0 7 9v6.25A1.75 1.75 0 0 1 5.25 17A3.25 3.25 0 0 1 2 13.75v-.25a3.5 3.5 0 0 1 3-3.465z"
							/></g
						></svg
					>Tanya Cs</button
				>
			</div>
		</div>
		<div id="come" class="ml-10 hidden">
			<p class="font-semibold text-white mb-4">
				Status Klinik <span class="bg-green-600 p-1 rounded-sm">Open</span>
			</p>
			<h1 class="text-5xl font-bold text-white mb-4">Dr. Muhammad Fifin Kombih</h1>
			<img src="jadwal.png" alt="jadwal" class="w-96" />
		</div>
		<div>
			<img src="img-hero.png" alt="dokter fifin" class="dr ml-28 hidden lg:block w-[27rem]" />
		</div>
	</div>
</section>
