<template>
  <div class="input-block">
    <v-alert 
    class="alert-box"
      border="bottom"
      dismissible
      v-show="copied"
    >
      Shortend URL is copied to clipboard
    </v-alert>
    <h3 class="text-h4 text-center mt-16">Paste Your URL to be Shortend</h3>
    <div class="url-area d-flex">
    <v-text-field v-model="url" label="Enter Url Here." single-line outlined @change="getShortenUrl"></v-text-field>
    <v-btn @click="getShortenUrl" :loading="loading"
       depressed class="py-7 ml-n1 " color="primary"> Shrink URL </v-btn>
</div>
    <div v-if="responseUrl" class="d-flex justify-center">
        <h3>Shortend URL: <a  :href= responseUrl target="_blank">{{responseUrl}}</a></h3>
    </div>
    
  </div>
</template>

<script>
import { store } from '@/store';
export default {
  name: "InputSection",
  
  data(){
    return{
        url: '',
        loading: false,
        copied: false
    }
  },
  methods:{
    getShortenUrl(){
        if(this.url.includes('https://')){
          this.loading = true
        store.dispatch("shortenUrl", this.url)
        setTimeout(()=>{
          this.loading = false 
        },3000)
        }
    },
    async copyURL(mytext) {
    try {
      await navigator.clipboard.writeText(mytext);
      this.copied = true
      setTimeout(()=>{
          this.copied = false 
        },4000)

    } catch($e) {
      alert('Cannot copy');
    }
  }
  },
  watch: {
responseUrl(){
  if(this.responseUrl && this.responseUrl.includes('https://')) {
    this.loading = false
    this.copyURL(this.responseUrl)
  }
}
  },
  computed: {
    responseUrl(){
        return store.state.shortenUrl
    }
  }

};
</script>

<style scoped>
.input-block{
   padding: 2rem;
   background-color: #f9f9f9;
   position: relative;
}
.url-area{
    width: 75%;
    margin: 1.5rem auto;
}
.alert-box{
  width: 18rem;
  position: absolute;
  top: 1rem;
  right: 2rem;
}
</style>