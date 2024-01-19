<!-- Main Content -->
<div class="flex-1">
	<!-- Main Content -->
	<div class="p-10">
		<!-- Your main content here -->
		<h1 class="text-xl font-bold">List Pasien</h1>

		<div class="container flex justify-end">
			<input type="text" placeholder="Type here" class="input input-bordered w-22 h-12" />
			<button class="btn bg-[#66D3D6] text-white font-semibold font-sm">CARI</button>
			<button
				><svg xmlns="http://www.w3.org/2000/svg" class="h-11 w-11 mx-2" viewBox="0 0 24 24"
					><path
						fill="currentColor"
						d="M18 7H6V3h12zm0 5.5q.425 0 .713-.288T19 11.5q0-.425-.288-.712T18 10.5q-.425 0-.712.288T17 11.5q0 .425.288.713T18 12.5M16 19v-4H8v4zm2 2H6v-4H2v-6q0-1.275.875-2.137T5 8h14q1.275 0 2.138.863T22 11v6h-4z"
					/></svg
				></button
			>
		</div>

		<div class="container bg-white mt-4 rounded-md">
			<div class="overflow-x-auto">
				<table class="table">
					<!-- head -->
					<thead>
						<tr>
							<th></th>
							<th>Tanggal</th>
							<th>No RM</th>
							<th>Nama</th>
							<th>TTL</th>
							<th>Instansi</th>
							<th>Aksi</th>
						</tr>
					</thead>
					<tbody>
						<!-- row 1 -->
						<tr>
							<th>1</th>
							<td>10-10-2024</td>
							<td>10002</td>
							<td>Galeh Ariya Irwana</td>
							<td>10-10-2002</td>
							<td>UNUSA</td>
							<td>
								<a href="/admin/rekam_medis/list" class="bg-[#FFBE00] p-1 text-white font-semibold rounded-sm"
									>Detail</a
								>
								|
								<a href="/admin/rekam_medis/add" class="bg-[#00A96E] p-1 text-white font-semibold rounded-sm"
									>Tambah</a
								>
							</td>
						</tr>
						<!-- row 2 -->
						<tr class="hover">
							<th>1</th>
							<td>10-10-2024</td>
							<td>10002</td>
							<td>Galeh Ariya Irwana</td>
							<td>10-10-2002</td>
							<td>UNUSA</td>
							<td>
								<a href="unusa.ac.id" class="bg-[#FFBE00] p-1 text-white font-semibold rounded-sm"
									>Detail</a
								>
								|
								<a href="unusa.ac.id" class="bg-[#00A96E] p-1 text-white font-semibold rounded-sm"
									>Tambah</a
								>
							</td>
						</tr>
						<!-- row 3 -->
						<tr>
							<th>1</th>
							<td>10-10-2024</td>
							<td>10002</td>
							<td>Galeh Ariya Irwana</td>
							<td>10-10-2002</td>
							<td>UNUSA</td>
							<td>
								<a href="unusa.ac.id" class="bg-[#FFBE00] p-1 text-white font-semibold rounded-sm"
									>Detail</a
								>
								|
								<a href="unusa.ac.id" class="bg-[#00A96E] p-1 text-white font-semibold rounded-sm"
									>Tambah</a
								>
							</td>
						</tr>
					</tbody>
				</table>
			</div>
		</div>
	</div>
</div>
