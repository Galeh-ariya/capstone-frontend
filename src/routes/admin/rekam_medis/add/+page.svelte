<script>
	import '../../../../app.css';
</script>

<section class=" w-full h-[510px] pt-20 p-10 flex justify-center items-center">
	<div class="card w-96 bg-base-100 shadow-xl">
		<div class="card-body font-semibold mx-4">
			<h2 class="card-title justify-center mb-6 text-[#6C757D]">Tambah Data</h2>
			<form action="">
				<input
					type="text"
					placeholder="Anamnesa"
					class="input input-bordered w-full max-w-xs text-[#6C757D]"
				/>
				<input
					type="text"
					placeholder="Diagnosa"
					class="input input-bordered w-full max-w-xs text-[#6C757D] mt-2"
				/>
                <input
						type="text"
						placeholder="Terapi"
						name="instansi"
						class="input input-bordered w-full max-w-xs mt-2"
					/>
					<input
						type="number"
						min="0"
						placeholder="Jumlah Obat"
						name="instansi"
						class="input input-bordered w-full max-w-xs mt-2"
					/>
				<div class="card-actions justify-center mt-4">
					<button
						class="btn bg-[#66D3D6] text-white w-full font-semibold">Tambah</button
					>
				</div>
			</form>
		</div>
	</div>
</section>


