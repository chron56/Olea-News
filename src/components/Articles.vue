<template>
  <div>
    <div class="line">  
      <button class="btn btn-outline-primary mr-1"  v-on:click="changeDataToGr">Ελληνικά</button>
      <button class="btn btn-outline-danger" v-on:click="changeDataToEn">English</button>  
    </div>
    <div class="container">
      <div class="card-columns">
        <div v-for="article in articles" v-bind:key="article.id" >
            <div class="card">
                <img class="card-img-top img-fluid"  v-bind:src=article.urlToImage>
                <div class="card-body">
                    <p class="card-text"> {{article.publishedAt | formatDate}}</p>
                    <h5 class="card-title">{{article.title}}</h5>
                    <p class="card-text">{{article.description}}</p>
                    <a v-bind:href=article.url class="btn btn-success" target="_blank">{{ readingButtonValue }} <i class="fas fa-external-link-alt"></i></a>   
                </div>
            </div>
        </div>  
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'

export default {
  name: 'Articles',
  data() {
    return {
      readingButtonValue:"Διάβασε το",
      articles:null,
      articlesGr: null,
      articlesEn: null,
    };
  },
  created: function() {
    var qGr="(λάδι OR λάδια OR ελαιόλαδο OR ελαιόλαδα OR ελιά OR ελιές OR ελαιοτριβείο OR ελαιοτριβεία OR λιοτρίβι OR λιοτρίβια OR ελαιόδεντρο OR ελαιόδεντρα)";
    var qEn="(olive AND oil)";
    var key="6c13096cfaaa4deba63de944f99549f8";
    axios
      .get('http://newsapi.org/v2/everything?qInTitle='+qGr+'&pageSize=100&sortBy=publishedAt&apiKey='+key)
      .then(res => {
        this.articlesGr = res.data.articles;
        this.articles=this.articlesGr;     
      });
    axios
      .get('http://newsapi.org/v2/everything?qInTitle='+qEn+'&language=en&pageSize=100&sortBy=publishedAt&apiKey='+key)
      .then(res => {
        this.articlesEn = res.data.articles;
      });     
  },
  methods: {
    changeDataToGr: function () {
      this.articles=this.articlesGr;
      this.readingButtonValue="Διάβασε το";
    },
    changeDataToEn: function () {
      this.articles=this.articlesEn;
      this.readingButtonValue="Read it";
    }
  },
  filters:{
    formatDate: function (value) {
      if (value) {
        return moment(String(value)).format('DD/MM/YYYY hh:mm')
      }
    }
  }
}
</script>

<style scoped>
  .line{
    margin-top:-20px;
    margin-bottom:20px;
    padding-top:10px;
    padding-bottom:10px;
    background-color: #e9ecef;
  }
</style>