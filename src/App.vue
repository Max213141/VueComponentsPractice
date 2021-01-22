

<template>
  <div>
    <div class="card">
      <h1>News from {{now}}</h1>
      <hr/>
      <span>U open {{ counter }} news | U read {{readNews}}</span>
    </div>

    <vue-news
      v-for="item in news"
      :key="item.id"
      :title="item.title"
      :id="item.id"
      :is-open="item.isOpen"
      :is-read="item.isRead"
      @news-open="open"
      @read-news="ReadThisNews"
    ></vue-news>

  </div>
</template>

<script>

  import VueNews from "@/VueNews";

  export default {
    data(){
      return{
        readNews:0,
        counter:0,
        now: new Date().toLocaleDateString(),
        news:[
          {
            title: '1 News',
            id:1,
            isOpen: false,
            isRead: false,
          },
          {
            title: '2 News',
            id:2,
            isOpen: false,
            isRead: false,
          },
        ]
      }
    },
    methods:{
      open(data){
        this.counter++
        console.log(data)
      },
      ReadThisNews(id){
        const news = this.news.find(news=> news.id === id)
        news.isRead = true
        this.readNews++
      }
    },
    provide(){
      return{
        title:'All news',
        news: this.news
      }
    },
    components:{
      'vue-news': VueNews
    }
  }
</script>
