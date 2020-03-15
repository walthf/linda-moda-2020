<template>
  <Layout>
    <div class="project">

      <div class="container">

        <div class="project-header">
          <h1 class="project-title" v-html="$page.post.title" />
          <div class="project-info">
            <div class="categories-container">
              <div class="categories">
                <span class="label">Marca</span>
                <span 
                  class="category"
                  v-for="(category, index) in $page.post.categories" 
                  :key="index"
                  v-text="category"
                />
              </div>
            </div>
            <div class="condition">
              <span class="label">Estado</span>
              <div v-html="$page.post.estado"/>
            </div>
            <div class="stock">
              <span class="label">Disponibilidad</span>
              <div v-html="$page.post.disponibilidad"/>
            </div>                                    
          </div>
          <div class="comprar">
              <span class="label">¿Dónde lo compro?</span>
              <a class="compra" :href="$page.post.compra_url" target="blank">Cómpralo en GOTRENDIER</a>
          </div>   
        </div>

        <div v-html="$page.post.content" class="content" />

      </div>

    </div>
  </Layout>
</template>

<page-query>
query ProjectPost ($path: String!) {
  post: projectPost (path: $path) {
    title
    date (format: "YYYY")
    content
    categories
    estado
    talla
    disponibilidad
    compra_url
    project_bg_color
    project_fg_color
    thumbnail (quality: 90)
  }
}
</page-query>
  
<script>
export default {
  metaInfo() {
    var windowVar = 'https://lindamodasustentable.com';
    return {
      ...this.$ogp({
        title: this.$page.post.title,
      description: this.$page.post.excerpt,
      image: windowVar + this.$page.post.thumbnail.src,
      appId: '821166215054888' // Facebook-only
    })
  }
}

}
</script>

<style scoped lang="scss">
.project-header {
  padding: 20vh 0 2rem 0;
}
.project-title {
  font-size: 4rem;
  margin: 0 0 4rem 0;
  padding: 0;
}
.project-info {
  display: flex;
  flex-wrap: wrap;
  font-size: 0.8rem;
  margin-bottom: 3rem;
}
.project-info > div {
  margin-right: 4rem;
  margin-bottom: 1rem;
}
.project-info > div:last-of-type {
  margin: 0;
}
.category:after {
  content: ', '
}
.category:last-of-type:after {
  content: '';
}
.comprar {
  font-size: 0.8rem;
  margin-bottom: 1rem;
  @media (max-width: 920px) {
    width: 100%;
    background-color: white;
    position: fixed;
    bottom: -1rem;
    right: 0;
    padding: .5rem;
    border-top: 1px solid #FC6767;
    .label {
      display:none;
    }
    .compra {
      width: 100%;
      text-align: center;
    }
  }
  .compra {
        background: linear-gradient(90deg, #EC008C 0%, #FC6767 100%);
        padding: 12px 16px;
        color: white;
        display: inline-block;
        transition: .2s ease;
        border: 0;
        text-decoration: none;
        // font-weight: 500;
        font-size: 16px;
        &:hover {
          box-shadow: -8px 8px black;
          // transform: translate(4px, -4px);
        }
      }
}
</style>
