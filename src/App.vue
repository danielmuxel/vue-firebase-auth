<template>
  <main>
    <Navbar />
    <section class="section">
      <div class="container">
        <router-view />
      </div>
    </section>
    <Footer />
  </main>
</template>

<script>
import Navbar from "./components/Navbar";
import Footer from "./components/Footer";

export default {
  components: {
    Navbar,
    Footer,
  },
};
</script>

<style>
/* Make footer stick to the bttom */
main {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

main > footer {
  margin-top: auto;
}
</style>