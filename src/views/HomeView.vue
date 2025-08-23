<template>
  <div class="home">
    <!-- ヒーローセクションの下のコンテンツエリア -->
    <div class="container mx-auto px-4 py-16">
      <!-- レシピ一覧タイトル -->
      <div class="text-center mb-12">
        <h2 class="text-2xl md:text-3xl font-bold mb-8 text-gray-800">
          レシピ一覧
        </h2>
        <p class="text-gray-600 max-w-2xl mx-auto">
          家族みんなで楽しめる、愛情たっぷりのレシピをご紹介します。
        </p>
      </div>

      <!-- カテゴリタブ -->
      <div class="flex justify-center mb-8">
        <div class="flex flex-wrap gap-4">
          <button
            v-for="category in categories"
            :key="category.id"
            @click="selectedCategory = category.id"
            :class="[
              'px-6 py-3 rounded-lg font-medium transition-all duration-400',
              selectedCategory === category.id
                ? 'bg-blue-500 text-white shadow-lg'
                : 'bg-gray-100 text-gray-700 hover:bg-gray-200',
            ]"
          >
            {{ category.name }}
          </button>
        </div>
      </div>

      <!-- レシピカード -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6 max-w-6xl mx-auto">
        <div
          v-for="recipe in filteredRecipes"
          :key="recipe.id"
          @click="openModal(recipe)"
          class="bg-white rounded-lg shadow-md overflow-hidden cursor-pointer hover:shadow-lg transition-all duration-200 hover:transform hover:-translate-y-2"
        >
          <!-- 料理画像 -->
          <div class="h-48 bg-gray-200 flex items-center justify-center">
            <img
              :src="recipe.image"
              :alt="recipe.name"
              class="w-full h-full object-cover"
              @error="handleImageError"
            />
          </div>
          <!-- 料理名 -->
          <div class="p-4">
            <h3 class="text-lg font-semibold text-gray-800">
              {{ recipe.name }}
            </h3>
          </div>
        </div>
      </div>

      <!-- モーダル -->
      <div
        v-if="selectedRecipe"
        @click="closeModal"
        class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-4"
      >
        <div
          @click.stop
          class="bg-white rounded-lg max-w-2xl w-full max-h-[90vh] overflow-y-auto"
        >
          <!-- モーダルヘッダー -->
          <div class="flex justify-between items-center p-6 border-b">
            <h2 class="text-2xl font-bold text-gray-800">
              {{ selectedRecipe.name }}
            </h2>
            <button
              @click="closeModal"
              class="text-gray-500 hover:text-gray-700 text-2xl"
            >
              ×
            </button>
          </div>

          <!-- モーダルコンテンツ -->
          <div class="p-6">
            <!-- 拡大された料理画像 -->
            <div class="mb-6">
              <img
                :src="selectedRecipe.image"
                :alt="selectedRecipe.name"
                class="w-full h-64 object-cover rounded-lg"
                @error="handleImageError"
              />
            </div>

            <!-- 料理の説明 -->
            <div class="mb-6">
              <h3 class="text-lg font-semibold mb-2">料理の説明</h3>
              <p class="text-gray-600">{{ selectedRecipe.description }}</p>
            </div>

            <!-- 材料 -->
            <div class="mb-6">
              <h3 class="text-lg font-semibold mb-3">材料</h3>
              <ul class="space-y-1">
                <li
                  v-for="ingredient in selectedRecipe.ingredients"
                  :key="ingredient"
                  class="text-gray-600"
                >
                  • {{ ingredient }}
                </li>
              </ul>
            </div>

            <!-- 作り方 -->
            <div>
              <h3 class="text-lg font-semibold mb-3">作り方</h3>
              <ol class="space-y-3">
                <li
                  v-for="(step, index) in selectedRecipe.steps"
                  :key="index"
                  class="flex"
                >
                  <span
                    class="bg-blue-500 text-white rounded-full w-6 h-6 flex items-center justify-center text-sm mr-3 mt-0.5"
                  >
                    {{ index + 1 }}
                  </span>
                  <span class="text-gray-600">{{ step }}</span>
                </li>
              </ol>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeView",
  data() {
    return {
      selectedCategory: "rice",
      selectedRecipe: null,
      categories: [
        { id: "rice", name: "米類" },
        { id: "noodles", name: "麺類" },
        { id: "dessert", name: "デザート" },
      ],
      recipes: [
        // 米類
        {
          id: 1,
          name: "牛丼",
          category: "rice",
          image: require("@/assets/gyudon.jpg"), // Image 1
          description:
            "甘辛いタレで煮込んだ牛肉とたまねぎをご飯の上にのせた、日本の代表的な丼料理です。",
          ingredients: [
            "牛切り落とし肉 300g",
            "たまねぎ 1個",
            "ご飯 2杯分",
            "しょうゆ 大さじ3",
            "みりん 大さじ2",
            "砂糖 大さじ1",
            "だし汁 150ml",
          ],
          steps: [
            "たまねぎを薄切りにします。",
            "フライパンにだし汁、しょうゆ、みりん、砂糖を入れて煮立てます。",
            "たまねぎを加えて3分ほど煮ます。",
            "牛肉を加えて色が変わるまで煮ます。",
            "ご飯の上に盛り付けて完成です。",
          ],
        },
        {
          id: 2,
          name: "カレー",
          category: "rice",
          image: require("@/assets/curry.jpg"), // Image 3
          description:
            "スパイスの効いた本格的なカレーライス。野菜と肉の旨味がたっぷり詰まった一品です。",
          ingredients: [
            "牛肉 300g",
            "じゃがいも 2個",
            "人参 1本",
            "たまねぎ 1個",
            "カレールー 1/2箱",
            "ご飯 適量",
            "水 600ml",
          ],
          steps: [
            "野菜を一口大に切ります。",
            "牛肉を炒めて取り出します。",
            "野菜を炒めてから水を加えて煮込みます。",
            "アクを取りながら20分煮込みます。",
            "カレールーを加えて10分煮込んで完成です。",
          ],
        },
        {
          id: 3,
          name: "炒飯",
          category: "rice",
          image: require("@/assets/chahan.jpg"), // Image 4
          description:
            "パラパラに仕上がった本格的な炒飯。卵とご飯の絶妙なバランスが美味しさの秘訣です。",
          ingredients: [
            "ご飯 2杯分",
            "卵 2個",
            "チャーシュー 100g",
            "長ねぎ 1/2本",
            "塩・こしょう 少々",
            "しょうゆ 小さじ1",
            "ごま油 大さじ1",
          ],
          steps: [
            "卵を溶いてご飯と混ぜておきます。",
            "フライパンを強火で熱し、卵ご飯を炒めます。",
            "チャーシューと長ねぎを加えて炒めます。",
            "塩、こしょう、しょうゆで味付けします。",
            "ごま油で香りをつけて完成です。",
          ],
        },
        // 麺類
        {
          id: 4,
          name: "ラーメン",
          category: "noodles",
          image: require("@/assets/ramen.jpg"), // Image 6
          description:
            "コク深いスープと麺の絶妙なバランスが楽しめる本格ラーメンです。",
          ingredients: [
            "ラーメン麺 1玉",
            "チャーシュー 3枚",
            "メンマ 適量",
            "煮卵 1個",
            "ねぎ 適量",
            "のり 1枚",
            "ラーメンスープ 300ml",
          ],
          steps: [
            "スープを温めておきます。",
            "麺を茹でます。",
            "どんぶりにスープを入れます。",
            "茹でた麺をどんぶりに入れます。",
            "トッピングをのせて完成です。",
          ],
        },
        {
          id: 5,
          name: "うどん",
          category: "noodles",
          image: require("@/assets/udon.jpg"), // Image 8
          description:
            "もちもちの讃岐うどんに温かいだしをかけた、心温まる一杯です。",
          ingredients: [
            "うどん 1玉",
            "かまぼこ 2切れ",
            "わかめ 適量",
            "ねぎ 適量",
            "だし汁 300ml",
            "しょうゆ 大さじ1",
            "みりん 小さじ1",
          ],
          steps: [
            "だし汁を温め、調味料を加えます。",
            "うどんを茹でます。",
            "茹でたうどんをどんぶりに入れます。",
            "温かいだし汁をかけます。",
            "トッピングをのせて完成です。",
          ],
        },
        {
          id: 6,
          name: "焼きそば",
          category: "noodles",
          image: require("@/assets/yakisoba.jpg"), // Image 9
          description:
            "ソースの香りが食欲をそそる、野菜たっぷりの焼きそばです。",
          ingredients: [
            "焼きそば麺 1玉",
            "キャベツ 100g",
            "もやし 50g",
            "豚バラ肉 80g",
            "焼きそばソース 大さじ2",
            "サラダ油 大さじ1",
            "青のり 適量",
          ],
          steps: [
            "キャベツを一口大に切り、豚肉は食べやすい大きさに切ります。",
            "フライパンに油を熱し、豚肉を炒めます。",
            "キャベツ、もやしを加えて炒めます。",
            "焼きそば麺を加えて炒め合わせます。",
            "焼きそばソースで味付けし、青のりをかけて完成です。",
          ],
        },
        // デザート
        {
          id: 7,
          name: "クッキー",
          category: "dessert",
          image: require("@/assets/cookies.jpg"), // Image 2
          description: "サクサクの食感と優しい甘さが特徴の手作りクッキーです。",
          ingredients: [
            "薄力粉 200g",
            "バター 100g",
            "砂糖 80g",
            "卵 1個",
            "バニラエッセンス 少々",
          ],
          steps: [
            "バターと砂糖をクリーム状に混ぜます。",
            "卵とバニラエッセンスを加えます。",
            "薄力粉を加えてひとまとめにします。",
            "形を整えて180℃のオーブンで12分焼きます。",
            "冷まして完成です。",
          ],
        },
        {
          id: 8,
          name: "パンケーキ",
          category: "dessert",
          image: require("@/assets/pancake.jpg"), // Image 5
          description:
            "ふわふわでもちもちの食感が楽しめる、優雅な朝食やおやつにぴったりのパンケーキです。",
          ingredients: [
            "ホットケーキミックス 200g",
            "牛乳 150ml",
            "卵 1個",
            "バター 適量",
            "メープルシロップ 適量",
            "生クリーム 適量",
          ],
          steps: [
            "ホットケーキミックスに牛乳と卵を加えて混ぜます。",
            "フライパンにバターを熱します。",
            "生地を流し入れて弱火で焼きます。",
            "表面に泡が出てきたらひっくり返します。",
            "生クリームとシロップをかけて完成です。",
          ],
        },
      ],
    };
  },
  computed: {
    filteredRecipes() {
      return this.recipes.filter(
        (recipe) => recipe.category === this.selectedCategory
      );
    },
  },
  methods: {
    openModal(recipe) {
      this.selectedRecipe = recipe;
    },
    closeModal() {
      this.selectedRecipe = null;
    },
    handleImageError(event) {
      // 画像が読み込めない場合のフォールバック
      event.target.src =
        "data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAwIiBoZWlnaHQ9IjMwMCIgdmlld0JveD0iMCAwIDQwMCAzMDAiIGZpbGw9Im5vbmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CjxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iMzAwIiBmaWxsPSIjRjNGNEY2Ii8+CjxyZWN0IHg9IjE1MCIgeT0iMTEwIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjgwIiBmaWxsPSIjRTVFN0VCIi8+CjxjaXJjbGUgY3g9IjE3NSIgY3k9IjEzNSIgcj0iMTUiIGZpbGw9IiNEMUQ1REIiLz4KPHBhdGggZD0iTTE2MiAxNTVMMTc1IDE0Mkw2ODcgMTY4TDE5OSAxNTVIMTYyWiIgZmlsbD0iI0QxRDVEQiIvPgo8L3N2Zz4=";
    },
  },
};
</script>
