<template>
  <div class="flex flex-col min-h-screen">
    <div class="flex-grow md:flex">
      <aside class="w-100 md:w-1/6 p-4 bg-gray-800 pt-8 pl-6 pr-6">
        <h1 class="p-0 mb-4 text-2xl font-extrabold text-white">
          MicroSaaS Affiliate Programs
        </h1>
        <h2 class="text-md mb-2 text-gray-100">Filter by Commission</h2>
        <select
          v-model="filterCommission"
          class="w-full p-2 border rounded bg-white text-white bg-gray-800"
        >
          <option value="">All</option>
          <option value="15">15%</option>
          <option value="20">20%</option>
          <option value="25">25%</option>
          <option value="30">30%</option>
          <option value="45">45%</option>
          <option value="50">50%</option>
        </select>
        <br /><br />
        <h2 class="text-md mb-2 text-gray-100">Filter by Lifetime</h2>
        <select
          v-model="filterLifetime"
          class="w-full p-2 border rounded bg-white text-white bg-gray-800"
        >
          <option value="">All</option>
          <option value="recurring">Recurring</option>
          <option value="12">12 Months</option>
          <option value="onceoff">Once Off</option>
        </select>
        <br /><br />
        <h2 class="text-md mb-2 text-gray-100">Filter by Category</h2>
        <select
          v-model="filterCategory"
          class="w-full p-2 border rounded bg-white text-white bg-gray-800"
        >
          <option value="">All</option>
          <option value="ai">AI</option>
          <option value="seo">SEO</option>
          <option value="social">Social Media</option>
          <option value="marketing">Marketing</option>
        </select>
      </aside>
      <!-- Your existing code -->
      <div class="w-full md:w-5/6 bg-gray-100">
        <!-- <h1 class="p-4 mt-3 mb-0 pb-1 text-3xl font-extrabold text-slate-900">
          MicroSaaS Affiliate Programs
        </h1> -->
        <p class="mt-6 font-bold pl-7">{{ filteredApps.length }} results</p>
        <div class="flex flex-wrap pl-4 pr-4">
          <div
            v-for="app in filteredApps"
            :key="app.name"
            class="w-full md:w-1/2 lg:w-1/3 p-4"
          >
            <div class="flex items-start p-2 bg-white rounded shadow">
              <img
                :src="app.logo ? app.logo : app.url + '/favicon.ico'"
                class="w-12 h-12 ml-2 mr-3 p-1"
                alt="logo"
              />
              <div>
                <h2 class="text-xl font-semibold">
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
        <div class="p-7">
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
        <!-- Footer -->
        <footer class="p-4 bg-gray-800 text-center text-white">
          Made with ❤️ by
          <a
            href="https://easyretro.io"
            target="_blank"
            class="text-blue-500 hover:underline"
            >EasyRetro</a
          >
        </footer>
      </div>
    </div>
  </div>
</template>

<script>
import { programs } from './_programs'

export default {
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
