<template>
  <div class="post-card">
    <div class="post-card__header">
      <g-image :alt="post.title" v-if="post.cover_image" class="post-card__image" :src="post.cover_image"/>
    </div>
    <div class="post-card__content">
      <h4 class="post-card__title" v-html="post.title" />
      <p class="post-card__description" v-html="post.description" />
    </div>
    <g-link class="post-card__link" :to="post.path">Link</g-link>
  </div>
</template>



<script>

export default {
  props: ['post'],
}
</script>

<style scoped>
  .post-card {
    background-color: var(--color-light);
    position: relative;
  }

    .post-card:hover {
      transform: translateY(-3px);
      box-shadow: 0 5px 10px rgba(0,0,0,0.1);
    }

    .post-card h4 {
      padding-top: calc(var(--space)/2);
      text-transform: none;
      font-weight: 500;
      letter-spacing: 0;
      text-align: left;
    }


    .post-card__link {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      opacity: 0.0;
      overflow: hidden;
      text-indent: -9999px;
      z-index: 0;
    }

    .post-card__header {
      margin-bottom: calc(var(--space)/2);
    }
      .post-card__header img {
        display:block;
      }
    
    .post-card__content {
      padding-left: calc(var(--space)/2);
      padding-right: calc(var(--space)/2);
      padding-bottom: calc(var(--space)/2);
      font-size: 90%;
      text-align: left;
    }

     .post-card__content h4 {
        margin-bottom: calc(var(--space)/2);
      }
    

    .post-card__description {
      margin-bottom: 0;
      font-size: calc(var(--base-font-size)*0.9);
    }
  
</style>
