<!-- Main Content -->

	<!-- Main Content -->
	<div class="p-10">
		<!-- Your main content here -->
		<h1 class="text-xl font-bold">Menambah Pasien</h1>

		<section class="w-full h-full pt-20 p-10 flex justify-center items-center">
			<div class="card w-full bg-base-100 shadow-xl">
				<div class="card-body font-semibold mx-4">
					<form action="">
						<div class="flex relative">
							<div>
								<input
									type="text"
									placeholder="Nama"
									name="nama"
									class="input input-bordered w-full max-w-xs"
								/>
								<input
									type="text"
									placeholder="E-mail"
									name="E-mail"
									class="input input-bordered w-full max-w-xs"
								/>
								<input
									type="text"
									placeholder="Jenis Kelamin"
									name="Jenis Kelamin"
									class="input input-bordered w-full max-w-xs"
								/>
								<input
									type="text"
									name="tempat_lahir"
									placeholder="Tempat Lahir"
									class="input border-[#cdc9c9] mt-2 w-28 textarea-xs"
								/>
								<input
									type="date"
									name="tanggal_lahir"
									placeholder="tanggal Lahir"
									class="input border-[#cdc9c9] mt-2 w-28"
								/>
								<input
									type="text"
									placeholder="Instansi"
									name="instansi"
									class="input input-bordered w-full max-w-xs mt-2"
								/>
								<select class="select select-bordered w-full max-w-xs mt-2" name="kategori">
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
									name="instansi"
									class="input input-bordered w-full max-w-xs mt-2"
								/>
								<input
									type="text"
									placeholder="Diagnosa"
									name="instansi"
									class="input input-bordered w-full max-w-xs mt-2"
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
								<div class="card-actions justify-end mt-2">
							<button class="btn btn-accent text-white">Simpan</button>
							</div>
						</div>
					</form>
				</div>
			</div>
		</section>
	</div>

