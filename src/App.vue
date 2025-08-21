<template>
  <div id="app">
    <!-- 全ページ共通のヘッダーナビゲーション -->
    <header class="bg-white shadow-sm">
      <nav
        class="container mx-auto flex justify-between items-center px-4 py-4"
      >
        <router-link
          to="/"
          class="text-3xl md:text-4xl font-bold text-gray-800 hover:text-gray-600 transition-colors"
        >
          レシピサイト
        </router-link>
        <router-link
          to="/about"
          class="text-xl md:text-2xl text-blue-600 hover:text-blue-800 hover:underline transition-all duration-200"
        >
          about
        </router-link>
      </nav>
    </header>

    <!-- ヒーローセクション（ホームページのみ表示） -->
    <div v-if="$route.path === '/'" class="hero-section">
      <div class="relative h-screen flex items-top justify-center">
        <!-- 背景画像 -->
        <div class="absolute inset-0">
          <img
            src="@/assets/rice1.jpg"
            alt="美味しい料理"
            class="w-full h-full object-cover"
          />
          <!-- 画像上部の黒いオーバーレイ -->
          <div
            class="absolute inset-0 bg-gradient-to-b from-black/70 via-black/30 to-transparent"
          ></div>
        </div>

        <!-- テキストコンテンツ -->
        <div class="relative z-10 text-center text-white px-4 pt-24">
          <h1
            class="text-4xl md:text-6xl lg:text-7xl font-bold mb-4 md:mb-6 leading-tight"
          >
            おいしい料理の世界
          </h1>
          <p
            class="text-lg md:text-xl lg:text-2xl font-light opacity-90 max-w-3xl mx-auto"
          >
            心を込めて作る、家族みんなが喜ぶ料理たち
          </p>
        </div>
      </div>
    </div>

    <!-- 各ページのコンテンツ -->
    <main>
      <router-view />
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>
