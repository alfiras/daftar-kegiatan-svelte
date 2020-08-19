<script>
  let daftar = [];
  let kegiatanInput = "";
  let kegiatanUbahID = "";
  let kegiatanUbah = "";
  let isUbah = false;

  $: dataTampil = daftar;

  const cariKegiatan = (e) => {
    e.target.value !== ""
      ? (dataTampil = daftar.filter((d) => d.kegiatan.includes(e.target.value)))
      : (dataTampil = daftar);
  };

  const tambahKegiatan = () => {
    daftar = [...daftar, { id: daftar.length + 1, kegiatan: kegiatanInput }];
    kegiatanInput = "";
  };

  const ubahKegiatan = (df) => {
    isUbah = true;
    kegiatanUbahID = df.id;
    kegiatanUbah = df.kegiatan;
  };

  const ubahKegiatanCommit = () => {
    isUbah = false;
    daftar = [
      ...daftar.map((d) => {
        d.id === kegiatanUbahID ? (d.kegiatan = kegiatanUbah) : null;
        return d;
      }),
    ];
  };

  const hapusKegiatan = (df) => {
    daftar = daftar.filter((d) => d.id !== df.id);
  };
</script>

<!-- <main>Halo Dunia</main> -->
<div
  class="min-h-screen bg-gray-100 flex flex-row justify-center items-start p-10">
  <div class="bg-white pt-3 rounded shadow-xl w-1/2">
    <div class="px-3 mb-2">
      <span class="tracking-wide leading-normal text-lg text-gray-800">
        Daftar Kegiatan
      </span>
    </div>

    <form on:submit|preventDefault={tambahKegiatan}>
      <div class="px-3 flex flex-row pb-4 mb-2">
        <div class="relative flex-grow flex text-gray-400">
          <input
            class="bg-gray-100 focus:bg-white focus:border-gray-200 border p-2
            flex-grow mr-2 rounded appearance-none focus:outline-none pl-5
            text-black"
            placeholder="Masukan Kegiatan baru"
            bind:value={kegiatanInput} />
          <span class="absolute inset-y-0 left-0 flex items-center">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 24 24"
              class="icon-add w-6 h-6 fill-current">
              <path
                class="secondary"
                fill-rule="evenodd"
                d="M17 11a1 1 0 0 1 0 2h-4v4a1 1 0 0 1-2 0v-4H7a1 1 0 0 1
                0-2h4V7a1 1 0 0 1 2 0v4h4z" />
            </svg>
          </span>
        </div>
        <button
          type="submit"
          class="text-lg bg-blue-500 p-2 rounded shadow-lg text-white">
          Tambah Kegiatan
        </button>
      </div>
    </form>

    <div class="bg-gray-100 py-3 rounded-b">
      <div class="px-3 mb-2 flex flex-row justify-end">
        <div class="relative">
          <input
            class="bg-gray-100 focus:bg-white focus:border-gray-200 border p-1
            rounded appearance-none focus:outline-none pl-5 "
            placeholder="Cari Kegiatan"
            on:keyup={cariKegiatan} />

          <span class="absolute inset-y-0 left-0 flex items-center pl-1">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 24 24"
              class="icon-search w-4 h-4 fill-current text-gray-100
              focus:text-black">
              <circle cx="10" cy="10" r="7" class="primary" />
              <path
                class="secondary fill-current text-gray-400"
                d="M16.32 14.9l1.1 1.1c.4-.02.83.13 1.14.44l3 3a1.5 1.5 0 0
                1-2.12 2.12l-3-3a1.5 1.5 0 0 1-.44-1.14l-1.1-1.1a8 8 0 1 1
                1.41-1.41zM10 16a6 6 0 1 0 0-12 6 6 0 0 0 0 12z" />
            </svg>
          </span>
        </div>
      </div>

      <div class="px-3 flex flex-col">

        {#if isUbah}
          <div
            class="flex flex-row w-100 mb-2 py-1 justify-between items-center">
            <input
              class="bg-gray-100 focus:bg-white focus:border-gray-200 border p-2
              flex-grow rounded appearance-none focus:outline-none mr-2"
              placeholder="Tekan Enter untuk mengubah kegiatan"
              bind:value={kegiatanUbah}
              disabled={!isUbah} />
            <div class="flex flex-row">

              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                class="icon-edit w-4 h-4 mr-2 fill-current text-gray-400
                hover:text-blue-500 cursor-pointer"
                on:click={ubahKegiatanCommit}>
                <path
                  class="primary"
                  d="M4 14a1 1 0 0 1 .3-.7l11-11a1 1 0 0 1 1.4 0l3 3a1 1 0 0 1 0
                  1.4l-11 11a1 1 0 0 1-.7.3H5a1 1 0 0 1-1-1v-3z" />
                <rect
                  width="20"
                  height="2"
                  x="2"
                  y="20"
                  class="secondary"
                  rx="1" />
              </svg>
            </div>
          </div>
        {/if}

        {#each dataTampil as d}
          <div
            class="flex flex-row w-100 mb-2 py-1 justify-between items-center">
            <span class="leading-normal tracking-wide text-lg text-gray-800">
              {d.kegiatan}
            </span>
            {#if !isUbah}
              <div class="flex flex-row">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 24 24"
                  class="icon-edit w-4 h-4 mr-2 fill-current text-gray-400
                  hover:text-blue-500 cursor-pointer"
                  on:click={ubahKegiatan(d)}>
                  <path
                    class="primary"
                    d="M4 14a1 1 0 0 1 .3-.7l11-11a1 1 0 0 1 1.4 0l3 3a1 1 0 0 1
                    0 1.4l-11 11a1 1 0 0 1-.7.3H5a1 1 0 0 1-1-1v-3z" />
                  <rect
                    width="20"
                    height="2"
                    x="2"
                    y="20"
                    class="secondary"
                    rx="1" />
                </svg>
                <!-- svg ubah -->
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 24 24"
                  class="icon-trash w-4 h-4 fill-current text-gray-400
                  hover:text-red-500 cursor-pointer"
                  on:click={hapusKegiatan(d)}>
                  <path
                    class="primary"
                    d="M5 5h14l-.89 15.12a2 2 0 0 1-2 1.88H7.9a2 2 0 0
                    1-2-1.88L5 5zm5 5a1 1 0 0 0-1 1v6a1 1 0 0 0 2 0v-6a1 1 0 0
                    0-1-1zm4 0a1 1 0 0 0-1 1v6a1 1 0 0 0 2 0v-6a1 1 0 0 0-1-1z" />
                  <path
                    class="secondary"
                    d="M8.59 4l1.7-1.7A1 1 0 0 1 11 2h2a1 1 0 0 1 .7.3L15.42
                    4H19a1 1 0 0 1 0 2H5a1 1 0 1 1 0-2h3.59z" />
                </svg>
                <!-- svg hapus -->
              </div>
            {/if}
          </div>
        {:else}
          <p class="text-center">
            <b>Tidak Ada Kegiatan</b>
          </p>
        {/each}

      </div>

    </div>
  </div>
</div>
