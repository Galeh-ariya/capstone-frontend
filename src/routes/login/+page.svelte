<script>
	import './login.css';
	import '../../app.css';
	import { onMount } from 'svelte';

	/**
	 * @type {HTMLElement | null}
	 */
	let modal;

	onMount(() => {
		const humberger = document.querySelector('#humberger');
		const navMenu = document.querySelector('#nav-menu');
		modal = document.getElementById(`my_modal_1`);

		humberger?.addEventListener('click', function () {
			humberger.classList.toggle('humb-active');
			navMenu?.classList.toggle('hidden');
		});
	});

	const reqBody = {
		email: '',
		password: ''
	};

	const loginHandle = async () => {
		fetch('http://localhost:8080/api/auth/login', {
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
				if (data.data.role == 1) {
					location.href = '/admin?message=' + data.data.token;
				} else {
					location.href = '/rm?message=' + data.data.token;
				}
				console.log(data.data.email);
			})
			.catch((err) => {
				// @ts-ignore
				modal.showModal();
				// console.log(err);
			});
	};
</script>

<dialog id="my_modal_1" class="modal">
	<div class="modal-box">
		<h3 class="font-bold text-lg text-red-600">Failed!</h3>
		<p class="py-4">Email atau Password Salah!</p>
		<svg xmlns="http://www.w3.org/2000/svg" class="w-32 h-32 animate-bounce text-red-600 mt-10 mx-auto" viewBox="0 0 512 512"
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

<header
	class="absolute top-0 left-0 w-full flex items-center justify-center z-10 shadow-md bg-white"
>
	<div class="container">
		<div class="flex items-center justify-between relative">
			<div class="px-4">
				<img src="Logo_Klinik.png" alt="unusa" class="w-16 py-6 block" />
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
			<form on:submit|preventDefault={loginHandle}>
				<input
					type="text"
					placeholder="Email"
					class="input input-bordered w-full max-w-xs text-[#6C757D] mb-5"
					name="email"
					bind:value={reqBody.email}
				/>
				<input
					type="password"
					placeholder="Password"
					class="input input-bordered w-full max-w-xs text-[#6C757D] mb-5"
					name="password"
					bind:value={reqBody.password}
				/>
				<div class="card-actions justify-center">
					<button
						type="submit"
						name="submit"
						class="btn bg-[#66D3D6] text-white w-full font-semibold">LOGIN</button
					>
				</div>
			</form>
		</div>
	</div>
</section>

<!-- <button class="btn" onclick="my_modal_1.showModal()">open modal</button> -->
