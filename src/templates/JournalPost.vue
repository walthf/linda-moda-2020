<template>
  <Layout>
    <div class="journal">
      <div class="container journal-container">

        <div class="journal-header">
          <h1 v-html="$page.post.title" class="journal-title" />
          <div class="journal-meta">
            <div class="journal-author">
              <span class="label">Autor</span>
              <span class="author-name" v-text="$page.post.author" />
            </div>
            <div class="journal-date">
              <span class="label">Fecha</span>
              <div v-text="$page.post.date"/>
            </div>
            <div class="journal-time">
              <span class="label">Tiempo</span>
              <span>{{ $page.post.timeToRead }} minutos de lectura</span>
            </div>
          </div>          
        </div>

        <JournalContent :content="$page.post.content" />

      </div>
    </div>
  </Layout>
</template>

<page-query>
query JournalPost ($path: String!) {
  post: journalPost (path: $path) {
    title
    author
    date (format: "D. MMMM YYYY")
    timeToRead
    content
    excerpt
    thumbnailjournal
  }
}
</page-query>

<script>
import JournalContent from "@/components/JournalContent"

export default {
  components: {
    JournalContent
  },
  metaInfo() {
    var windowVar = 'https://lindamodasustentable.com';
  return {
    ...this.$ogp({
      title: this.$page.post.title,
      description: this.$page.post.excerpt,
      image: windowVar + this.$page.post.thumbnailjournal.src,
      appId: '821166215054888' // Facebook-only
    })
  }
}
}
</script>

<style scoped>
.journal-container {
  max-width: 840px;
}
.journal-header {
  padding: 20vh 0 4rem 0;
}
.journal-title {
  font-size: 4rem;
  margin: 0 0 4rem 0;
  padding: 0;
}
.journal-meta {
  display: flex;
  flex-wrap: wrap;
  font-size: 0.8rem;
}
.journal-meta > div {
  margin-right: 4rem;
  margin-bottom: 1rem;
}
.journal-meta > div:last-of-type {
  margin: 0;
}
</style>
