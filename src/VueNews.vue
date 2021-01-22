<template>
  <div class="card">
    <h2>{{title}}</h2>
    <hr/>
    <app-button
        @action="open"
    >{{thereIsOpen ? 'Close' : 'Open'}}</app-button>

    <div v-if="thereIsOpen">
      <p>Lorem ipsum dolor sit amet.</p>
      <app-button
          color="primary"
          v-if="!isRead"
          @action="readNews"
      >Read News</app-button>

      <app-news-list></app-news-list>
    </div>

  </div>
</template>

<script>
import AppButton from "@/AppButton";
import AppNewsList from "@/AppNewsList";
  export default {
    emits:{
      'news-open': null,
      'read-news'(id){
        if(id){
          return true
        }
        console.log('no id for read-news emit')
        return false
      }
    },
    props:{
      title:{
        type:String,
      },
      id:{
        type:Number,
        required: true
      },
      isOpen:{
        type:Boolean,
        required:false,
        default: true,
        validator(value){
          console.log(value)
          return true
        }
      },
      isRead:Boolean,
    },
    data(){
      return {
        thereIsOpen:this.isOpen
      }
    },
    methods:{
      open(){
        this.thereIsOpen=!this.thereIsOpen
        if(this.thereIsOpen){
          this.$emit('news-open', 22)
        }
      },
      readNews(){
        this.thereIsOpen = false
        this.$emit('read-news', this.id)
      }
    },
    components:{AppButton,AppNewsList}
  }
</script>