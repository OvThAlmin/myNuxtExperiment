<template>
    <section class="container">
        <div class="columns is-multiline">
            <!-- v-for で breed_list からループ出力 -->
            <div v-for="(item, i) in breed_list" v-bind:key='i' class='column is-2'>
                <nuxt-link :to="{ path: 'dogs/'+ i }" class="button">{{ i }}</nuxt-link>
            </div>
        </div>
    </section>
</template>

<script>
import catApi from '@/api/cat'
import {mapState} from 'vuex';

export default {
  async fetch({store}) {
            let json = await catApi.breeds();
            store.commit('breed_list_update', json)
  },
  computed: mapState(['breed_list']),  // mapState ヘルパー
}

</script>

<style>

.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
