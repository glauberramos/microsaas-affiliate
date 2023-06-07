<template>
  <div class="flex flex-col min-h-screen">
    <div class="flex-grow md:flex">
      <aside
        class="w-100 md:w-1/6 p-4 bg-gray-800 pt-8 pl-6 pr-6 md:sticky md:self-start md:min-h-screen md:top-0 md:flex flex-col"
      >
        <h1 class="p-0 mb-4 text-2xl font-extrabold text-white">
          MicroSaaS Affiliate Programs
        </h1>
        <h2 class="text-md mb-2 mt-2 md:mt-0 text-gray-100">
          Filter by Commission
        </h2>
        <select
          v-model="filterCommission"
          class="w-full p-2 border rounded text-white bg-gray-800"
        >
          <option value="">All</option>
          <option value="15">15%</option>
          <option value="20">20%</option>
          <option value="25">25%</option>
          <option value="30">30%</option>
          <option value="40">40%</option>
          <option value="45">45%</option>
          <option value="50">50%</option>
        </select>
        <br />
        <h2 class="text-md mb-2 mt-2 md:mt-0 text-gray-100">
          Filter by Lifetime
        </h2>
        <select
          v-model="filterLifetime"
          class="w-full p-2 border rounded text-white bg-gray-800"
        >
          <option value="">All</option>
          <option value="recurring">Recurring</option>
          <option value="12">12 Months</option>
          <option value="onceoff">Once Off</option>
        </select>
        <br />
        <h2 class="text-md mb-2 mt-2 md:mt-0 text-gray-100">
          Filter by Category
        </h2>
        <select
          v-model="filterCategory"
          class="w-full p-2 border rounded text-white bg-gray-800"
        >
          <option value="">All</option>
          <option value="ai">AI</option>
          <option value="seo">SEO</option>
          <option value="social">Social Media</option>
          <option value="marketing">Marketing</option>
        </select>
        <a
          class="px-4 py-2 text-white bg-blue-500 rounded hover:bg-blue-600 mb-2 mt-4 md:mt-7 text-center inline-block"
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
      <!-- Your existing code -->
      <div class="w-full md:w-5/6 bg-gray-100">
        <!-- <h1 class="p-4 mt-3 mb-0 pb-1 text-3xl font-extrabold text-slate-900">
          MicroSaaS Affiliate Programs
        </h1> -->
        <!-- <p class="mt-6 font-bold pl-7">{{ filteredApps.length }} results</p> -->
        <div class="flex flex-wrap pl-4 pr-4 pt-5">
          <div
            v-for="app in filteredApps"
            :key="app.name"
            class="w-full md:w-1/2 lg:w-1/3 p-4"
          >
            <div class="flex items-start p-2 bg-white rounded shadow pt-4 pb-3">
              <img
                :src="app.logo ? app.logo : app.url + '/favicon.ico'"
                class="w-12 h-12 ml-2 mr-3 p-1"
                alt="logo"
              />
              <div>
                <h2 class="text-lg font-semibold">
                  <a
                    :href="app.url"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="text-blue-500 hover:underline"
                    >{{ app.name }}</a
                  >
                </h2>
                <p class="text-gray-500">{{ app.description }}</p>

                <p class="text-sm text-gray-500 mt-1">
                  <strong>Commission: </strong
                  >{{
                    app.lifetime == 'onceoff'
                      ? app.type == 'percentage'
                        ? `${app.commission}%`
                        : `$${app.commission}.00`
                      : app.type == 'fixed'
                      ? `$${app.commission}.00`
                      : `${app.commission}%`
                  }}
                  <br />
                  <strong>Lifetime: </strong
                  >{{
                    app.lifetime == 'recurring'
                      ? 'Recurring'
                      : app.lifetime == 'onceoff'
                      ? 'Once Off'
                      : app.lifetime + ' months'
                  }}
                  <br />
                  <a
                    :href="app.programUrl"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="inline-block px-4 py-2 text-white bg-blue-500 rounded hover:bg-blue-600 mb-2 mt-3"
                    >Join Affiliate Program</a
                  >
                </p>
              </div>
            </div>
          </div>
        </div>
        <div class="p-7 pl-10 pr-10 max-w-4xl">
          <h2 class="text-2xl font-bold mb-2">What is MicroSaaS?</h2>
          <p class="mb-4">
            MicroSaaS is a unique subset of the Software as a Service (SaaS)
            model. MicroSaaS businesses are typically small, owner-operated
            companies that are highly specialized. They are often run by solo
            founders or small teams and serve a niche market.
          </p>
          <p class="mb-6">
            MicroSaaS businesses thrive by focusing on a narrow problem and
            providing a simple, effective solution. They typically require less
            capital to start and operate than larger SaaS businesses and can
            become profitable more quickly.
          </p>

          <h2 class="text-2xl font-bold mb-2">
            How do We Select our MicroSaaS Affiliate Programs?
          </h2>
          <p class="mb-4">
            We select MicroSaaS that are run by Indie Hackers, Bootstrapped
            Founders, Solopreneurs and Indie Makers. We prefer to select SaaS
            that are run by 1 person or a small team, that serves a specific
            niche, that are independent and don't have any external funding.
          </p>

          <h2 class="text-2xl font-bold mb-2">
            Benefits of Affiliate Programs
          </h2>
          <p class="mb-4">
            Affiliate programs offer an excellent opportunity to generate
            passive income. By promoting products or services, affiliates can
            earn a commission on any sales made through their referral link.
          </p>
          <p class="mb-6">
            These programs are particularly popular in the MicroSaaS space,
            where businesses are always looking for cost-effective ways to reach
            their target audience. Affiliates can help drive traffic and sales,
            making it a win-win for both parties.
          </p>

          <h2 class="text-2xl font-bold mb-2">
            Choosing the Right MicroSaaS Affiliate Program
          </h2>
          <p class="mb-4">
            When choosing an affiliate program, it's important to consider
            factors like the commission rate, payment terms, and the relevance
            of the product or service to your audience. It's also a good idea to
            use the product yourself so you can promote it authentically.
          </p>
          <p class="mb-6">
            Remember, the key to successful affiliate marketing is trust. Your
            audience needs to trust that you're recommending products because
            you genuinely believe they're valuable, not just because you're
            getting paid.
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { programs } from './_programs'

export default {
  head() {
    const metaTitle = 'Discover the latest microsaas affiliate programs'
    const metaDesc =
      'The biggest directory of microsaas affiliate programs by indie hackers, bootstrapped founders and solopreneurs.'

    const imageTitle = encodeURIComponent(metaTitle)
    const imageDescription = encodeURIComponent(metaDesc)
    const imageURL = `https://us-central1-funretro-pro.cloudfunctions.net/previewImage?text=${imageTitle}&desc=${imageDescription}`

    return {
      title: metaTitle,
      script: [
        {
          defer: true,
          dataDomain: 'microsaasaffiliate.com',
          src: 'https://plausible.io/js/script.js',
        },
      ],
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
        {
          hid: 'twitter:image',
          name: 'twitter:image',
          content: imageURL,
        },
        {
          hid: 'og:image',
          name: 'og:image',
          content: imageURL,
        },
        {
          hid: 'og:image:width',
          name: 'og:image:width',
          content: '1200',
        },
        {
          hid: 'og:image:height',
          name: 'og:image:height',
          content: '630',
        },
      ],
    }
  },
  data() {
    return {
      apps: programs,
      filterCommission: '',
      filterLifetime: '',
      filterCategory: '',
    }
  },
  computed: {
    filteredApps() {
      return this.apps
        .filter((app) =>
          this.filterCommission ? app.commission == this.filterCommission : true
        )
        .filter((app) =>
          this.filterCategory ? app.category == this.filterCategory : true
        )
        .filter((app) =>
          this.filterLifetime ? app.lifetime == this.filterLifetime : true
        )
    },
  },
}
</script>
