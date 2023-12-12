<template>
  <div id="app">
    <h2>Aplikasi Pengirim Paket</h2>
    <flowchart :nodes="nodes" :links="links"></flowchart>

    <div v-if="currentStep === 'input'">
      <h3>Langkah 1: Input Data Paket</h3>
      <button @click="submitData">Submit Data</button>
    </div>

    <div v-else-if="currentStep === 'process'">
      <h3>Langkah 2: Proses Pengiriman</h3>
      <p>Data Paket: {{ packageData }}</p>
      <button @click="deliverPackage">Proses Pengiriman</button>
    </div>

    <div v-else-if="currentStep === 'receive'">
      <h3>Langkah 3: Penerimaan Paket</h3>
      <p>Status Pengiriman: {{ deliveryStatus }}</p>
    </div>
  </div>
</template>

<script>
import Flowchart from 'flowchart-vue';

export default {
  components: {
    Flowchart,
  },
  data() {
    return {
      nodes: [
        { id: 'input', label: 'Input Data Paket', x: 100, y: 100 },
        { id: 'process', label: 'Proses Pengiriman', x: 200, y: 200 },
        { id: 'receive', label: 'Penerimaan Paket', x: 100, y: 300 },
      ],
      links: [
        { source: 'input', target: 'process', label: 'Submit Data' },
        { source: 'process', target: 'receive', label: 'Deliver Package' },
      ],
      currentStep: 'input',
      packageData: null,
      deliveryStatus: null,
    };
  },
  methods: {
    submitData() {
      this.packageData = {
        sender: 'John Doe',
        recipient: 'Jane Doe',
        contents: 'Important documents',
      };
      this.currentStep = 'process';
    },
    deliverPackage() {
      this.deliveryStatus = 'Paket berhasil dikirim';
      this.currentStep = 'receive';
    },
  },
};
</script>

<style>
#app {
  text-align: center;
  margin-top: 2em;
}
</style>
