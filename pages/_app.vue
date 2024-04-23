<template>
  <div id="home">
    <div>Hello world from your Vue project. Below is Builder Content:</div>

    <div v-if="content || isPreviewing()">
      <div>
        page title:
        {{ content?.data?.title || "Unpublished" }}
      </div>
      <Content
        model="page"
        :content="content"
        api-key="f1a790f8c3204b3b8c5c1795aeac4660"
      />
    </div>
    <div v-else>Content not Found</div>
  </div>
</template>

<script>
import { Content, fetchOneEntry, isPreviewing } from "@builder.io/sdk-vue";

// fetch builder content data
export default {
  components: {
    Content,
  },
  data: () => ({
    content: [],
  }),
  async fetch() {
    this.content = await fetchOneEntry({
      model: "page",
      apiKey: "f1a790f8c3204b3b8c5c1795aeac4660",
      userAttributes: { urlPath: this.$route.path },
    });
  },
};
</script>
