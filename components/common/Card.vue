<template>
  <section class="card">
    <nuxt-link :to="`/topics/${id}`" class="card__link">
      <div class="card__header">
        <h2 class="card__title">{{ title }}</h2>
        <p class="card__date">{{ date }}</p>
      </div>
      <img
        :src="img.fields.file.url"
        :alt="img.fields.description"
        class="card__img"
      />
    </nuxt-link>
  </section>
</template>

<script>
export default {
  props: {
    id: {
      type: String,
      required: true,
    },
    title: {
      type: String,
      required: true,
    },
    date: {
      type: String,
      required: true,
    },
    img: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style lang="scss" scoped>
.card {
  width: 320px;

  &__link {
    display: flex;
    flex-wrap: wrap;
  }

  &__header {
    display: flex;
    flex-direction: column;
    order: 1;
    width: 100%;
    padding: 1rem 0 0.5rem 0.5rem;
    overflow: hidden;
    transition: all 0.2s;
  }

  &__title {
    order: 1;
    width: 100%;
    margin-top: 0.5rem;
    overflow: hidden;
    font-size: 0.875rem;
    font-weight: bold;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  &__date {
    order: 0;
    width: 100%;
    font-size: 0.8rem;
    line-height: 1.5rem;
  }

  &__img {
    order: 0;
    width: 100%;
    height: 180px;
    object-fit: cover;
    border-radius: 10px 10px 0 0;
    transition: all 0.2s;
  }

  &__link:hover {
    .card__img {
      filter: grayscale(50%);
      border-radius: 10px;
      transition: all 0.3s;
      transform: scale(0.8, 0.8);
    }

    .card__header {
      color: #333;
      transition: all 0.3s;
      transform: scale(0.9, 0.9);
    }
  }
}
</style>
