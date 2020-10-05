<template>
  <section class="container">
    <header>
      <h1>Missões</h1>
    </header>
    <p v-if="$fetchState.pending">Fetching posts...</p>
    <p v-else-if="$fetchState.error">
      Error while fetching posts: {{ $fetchState.error.message }}
    </p>
    <div v-else class="card-container">
      <n-link
        v-for="mission of missions"
        :key="mission.name"
        class="card"
        :to="`/mission/${mission.id}`"
      >
        <div class="card-title">
          {{ mission.name }}
        </div>
        <div class="card-body"></div>
      </n-link>
    </div>
  </section>
</template>

<script>
import Logo from "~/components/Logo.vue";

export default {
  data() {
    return {
      missions: [],
    };
  },
  async fetch() {
    this.missions = await this.$axios.$get(
      "https://us-central1-teste-frontend-c2dcc.cloudfunctions.net/missions"
    );
  },
  components: {
    Logo,
  },
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
}

.card-container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.card {
  display: flex;
}

.title {
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
