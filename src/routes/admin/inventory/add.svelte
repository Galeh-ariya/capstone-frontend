<div class="container bg-transparent mt-4 rounded-md">
	<div class="flex justify-around">
		<div class="add">
			<div class="card w-96 bg-base-100 shadow-xl">
				<div class="card-body">
					<h2 class="card-title">Menambah Obat</h2>
					<form action="">
						<input
							type="text"
							placeholder="Nama Obat"
							name="name"
							class="input input-bordered w-full max-w-xs"
						/>
						<label class="form-control w-full max-w-xs mt-2">
							<div class="label">
								<span class="label-text">Kadaluarsa</span>
							</div>
							<input type="date" class="input input-bordered w-full max-w-xs" />
						</label>
						<input
							type="number"
							min="0"
							placeholder="Min Stok"
							name="name"
							class="input input-bordered w-full max-w-xs mt-2"
						/>
						<input
							type="number"
							min="0"
							placeholder="Stok Awal Bulan"
							name="name"
							class="input input-bordered w-full max-w-xs mt-2"
						/>
						<input
							type="number"
							min="0"
							placeholder="Jumlah Terpakai"
							name="name"
							class="input input-bordered w-full max-w-xs mt-2"
						/>
                        
						<div class="card-actions justify-end mt-2">
							<button class="btn btn-accent text-white">Simpan</button>
						</div>
					</form>
				</div>
			</div>
		</div>
		<div class="edit">
			<div class="card w-96 bg-base-100 shadow-xl">
				<div class="card-body">
					<h2 class="card-title">Mengubah Obat</h2>
					<p>If a dog chews shoes whose shoes does he choose?</p>
					<div class="card-actions justify-end">
						<button class="btn btn-primary">Buy Now</button>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>
