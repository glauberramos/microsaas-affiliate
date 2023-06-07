<template>
  <main id="main" class="home">
    <section class="top-section landing">
      <div class="grid-container">
        <div class="home-info flex-grow md:flex">
          <aside
            class="w-100 md:w-1/6 p-4 bg-gray-800 pt-8 pl-6 pr-6 md:sticky md:self-start md:min-h-screen md:top-0 md:flex flex-col"
          >
            <h1 class="p-0 mb-4 text-2xl font-extrabold text-white">
              MicroSaaS Affiliate Programs
            </h1>
            <a
              class="px-4 py-2 text-white bg-blue-500 rounded hover:bg-blue-600 mb-2 mt-4 text-center inline-block"
              href="https://docs.google.com/forms/d/e/1FAIpQLSeY2wbBy_Wuhhh32q74MtlfF9Ih_4cTci9T_hZkgjFyPfQUKg/viewform?usp=sf_link"
              target="_blank"
              >Submit a Program</a
            >
            <footer
              class="bg-gray-800 text-left md:text-center text-white text-sm mt-3 md:mt-auto"
            >
              Made with ❤️ by
              <a
                href="https://easyretro.io"
                target="_blank"
                class="text-blue-500 hover:underline"
                >EasyRetro</a
              >
            </footer>
          </aside>
          <div class="home-text">
            <div class="ml-8 mp-10">
              <h2 class="text-4xl font-semibold mb-4">
                <img
                  :src="
                    programData.logo
                      ? programData.logo
                      : programData.url + '/favicon.ico'
                  "
                  class="w-12 h-12 p-1 mt-8 mb-2"
                  alt="logo"
                />
                {{ programData.name }} Affiliate Program
              </h2>
              <p class="text-gray-500">{{ programData.description }}</p>

              <p class="text-gray-500 mt-4 mb-4">
                <strong>Commission: </strong
                >{{
                  programData.lifetime == 'onceoff'
                    ? programData.type == 'percentage'
                      ? `${programData.commission}%`
                      : `$${programData.commission}.00`
                    : programData.type == 'fixed'
                    ? `$${programData.commission}.00`
                    : `${programData.commission}%`
                }}
                <br />
                <strong>Lifetime: </strong
                >{{
                  programData.lifetime == 'recurring'
                    ? 'Recurring'
                    : programData.lifetime == 'onceoff'
                    ? 'Once Off'
                    : programData.lifetime + ' months'
                }}
                <br />
                <a
                  :href="programData.programUrl"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="inline-block px-4 py-2 text-white bg-blue-500 rounded hover:bg-blue-600 mb-2 mt-3 mr-2"
                  >Join Affiliate Program</a
                >
                <a
                  :href="programData.url"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="inline-block px-4 py-2 text-white bg-blue-500 rounded hover:bg-blue-600 mb-2 mt-3"
                  >Open Website</a
                >
              </p>
              <a class="underline mt-5 text-gray-500 inline-block" href="/"
                >Back to all affiliate programs</a
              >
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import { programs } from './../_programs'

export default {
  async asyncData({ params, redirect }) {
    const { program } = params

    for (let index in programs) {
      if (
        programs[index].name
          .toLowerCase()
          .split(' ')
          .join('-')
          .replace('.', '') === program
      ) {
        return {
          programData: programs[index],
        }
      }
    }

    return redirect('/error')
  },
  head() {
    const metaTitle = `${this.programData.name} Affiliate Program Information`
    const metaDesc = `${this.programData.name} Affiliate Program Information - Take a look into commision, lifetime and more.`

    return {
      title: metaTitle,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: metaDesc,
        },
        {
          hid: 'og:title',
          name: 'og:title',
          content: metaTitle,
        },
        {
          hid: 'og:description',
          name: 'og:description',
          content: metaDesc,
        },
        {
          hid: 'twitter:title',
          name: 'twitter:title',
          content: metaTitle,
        },
        {
          hid: 'twitter:description',
          name: 'twitter:description',
          content: metaDesc,
        },
      ],
    }
  },
}
</script>
