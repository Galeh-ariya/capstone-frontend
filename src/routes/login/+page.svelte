<script>
	import './login.css';
	import '../../app.css';
	import { onMount } from 'svelte';

	import { navigate } from 'svelte-routing';

	function pindahKeHalaman2() {
		navigate('/rm'); 
	}

	onMount(() => {
		const humberger = document.querySelector('#humberger');
		const navMenu = document.querySelector('#nav-menu');

		humberger?.addEventListener('click', function () {
			humberger.classList.toggle('humb-active');
			navMenu?.classList.toggle('hidden');
		});
	});
</script>

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
					</ul>
				</nav>
			</div>
		</div>
	</div>
</header>

<section class="mt-24 w-full h-[510px] pt-20 p-10 flex justify-center items-center">
	<div class="card w-96 bg-base-100 shadow-xl">
		<div class="card-body font-semibold mx-4">
			<h2 class="card-title justify-center mb-6 text-[#6C757D]">Login</h2>
			<form action="">
				<input
					type="text"
					placeholder="Email"
					class="input input-bordered w-full max-w-xs text-[#6C757D] mb-5"
				/>
				<input
					type="password"
					placeholder="Password"
					class="input input-bordered w-full max-w-xs text-[#6C757D] mb-5"
				/>
				<div class="card-actions justify-center">
					<button on:click={pindahKeHalaman2} class="btn bg-[#66D3D6] text-white w-full font-semibold">LOGIN</button>
				</div>
			</form>
		</div>
	</div>
</section>



