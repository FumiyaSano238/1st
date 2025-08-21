<template>
  <div id="app">
    <!-- 全ページ共通のヘッダーを追加 -->
    <div class="header">
      <nav class="flex justify-between p-4">
        <div class="text-2xl font-bold">レシピサイト</div>
        <router-link to="/about" class="text-blue-500 hover:underline">
          about
        </router-link>
      </nav>
    </div>

    <!-- 各ページのコンテンツ -->
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>
