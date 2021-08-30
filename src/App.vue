<template>
  <div id="app">
    <div class="table-responsive" style="margin-top:0rem;">
      <button class="btn btn-outline-primary btn-block" @click="reset()">Reset</button>
      <table class="table">
        <thead>
          <tr>
            <th>Intento</th>
            <th>Codigo</th>
            <th>Formato</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(scanner,index) in list_decoded_barcode" :key="index">
            <td>{{index}}</td>
            <td>{{scanner.codigo}}</td>
            <td>{{scanner.formato}}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="container" style="margin-bottom:1rem;">
      <Scanner :onDetected="logIt" :readerSize="readerSize" :readerTypes="['code_128_reader','ean_reader','ean_8_reader','code_39_reader','code_39_vin_reader','codabar_reader','upc_reader','upc_e_reader','i2of5_reader','2of5_reader','code_93_reader']"></Scanner>
    </div>
  </div>
</template>

<script>
import Scanner from './components/Scanner.vue'

export default {
  name: 'App',
  components: {
    Scanner
  },
  data () {
    return {
      list_decoded_barcode:[],
      readerSize: {
        width: 640,
        height: 480
      },
      detecteds: []
    }
  },
  methods: {
    logIt (data) {
      //console.log('detected', data)
      this.list_decoded_barcode.push({codigo:data.codeResult.code,formato:data.codeResult.format})
    },
    reset(){
      this.list_decoded_barcode = []
    }
  }
}
</script>

