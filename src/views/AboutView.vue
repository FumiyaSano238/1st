<template>
  <div class="about">
    <!-- 背景画像とコンテンツを含む全画面セクション -->
    <div class="relative min-h-screen">
      <!-- 背景画像 -->
      <div class="absolute inset-0">
        <img
          src="@/assets/pizza.jpg"
          alt="美味しいピザ"
          class="w-full h-full object-cover"
        />
        <!-- 右側のグラデーションオーバーレイ -->
        <div
          class="absolute inset-0 bg-gradient-to-r from-transparent via-black/30 to-black/70"
        ></div>
      </div>

      <!-- テキストコンテンツ（右側配置） -->
      <div class="relative z-10 flex items-center min-h-screen">
        <div class="w-full">
          <div class="ml-auto max-w-2xl px-6 md:px-12 lg:px-16 py-16">
            <!-- メインタイトル -->
            <h1
              class="text-4xl md:text-5xl lg:text-6xl font-bold mb-8 text-white leading-tight"
            >
              毎日をおいしく
            </h1>

            <!-- サブタイトルと説明文 -->
            <div class="space-y-6 text-white/90">
              <p class="text-xl md:text-2xl font-light">
                食べることが大好きな僕が<br />
                おいしそうだなと思ったレシピを
              </p>

              <p class="text-lg md:text-xl">vueとtailwindを使って作りました</p>

              <p class="text-base md:text-lg opacity-80">
                （ちなみに背景はバイトがピザ関係のため）
              </p>
            </div>

            <!-- 装飾的な区切り線 -->
            <div class="mt-12 mb-8">
              <div class="w-24 h-1 bg-white/50"></div>
            </div>

            <!-- 追加情報 -->
            <div class="text-white/80 space-y-4">
              <p class="text-lg">
                このサイトでは、家庭で作れる美味しいレシピを<br />
                カテゴリ別に分けてご紹介しています。
              </p>

              <p class="text-base">
                どの料理も愛情を込めて、<br />
                家族みんなが笑顔になれるような<br />
                レシピばかりです。
              </p>
            </div>

            <!-- 戻るボタン -->
            <div class="mt-12">
              <router-link
                to="/"
                class="inline-flex items-center px-8 py-3 bg-white/20 backdrop-blur-sm border border-white/30 text-white rounded-lg hover:bg-white/30 hover:border-white/50 transition-all duration-300"
              >
                <svg
                  class="w-5 h-5 mr-2"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M10 19l-7-7m0 0l7-7m-7 7h18"
                  ></path>
                </svg>
                レシピ一覧に戻る
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AboutView",
};
</script>
