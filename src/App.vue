<script>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import Map from './components/Map.vue'
import Table from './components/Table.vue'
import Donate from './components/Donate.vue'
import Resources from './components/Resources.vue'
import marilynJson from './assets/marilyns.json' assert {type: 'json'}

export default {
  name: "App",
  components: {
    Header,
    Footer,
    Map,
    Table,
    Donate,
    Resources,
  },
  data() {
    return {
      marilynData: marilynJson
    }
  }
};
</script>

<template>
  <Header/>
  <main class="container">
    <Map :marilyns="marilynData"/>
    <section class="grid">
      <Donate />
      <Resources />
    </section>
    <Table :marilyns="marilynData"/>
  </main>
  <Footer/>
</template>

