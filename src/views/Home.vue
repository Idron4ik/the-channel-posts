<template>
  <div class="post-categories">
    <div
        class="post-categories__item"
        v-for="(posts, category) in postCategories"
        :key="category"
    >
      <h2 class="post-categories__title">{{category}}</h2>
      <ul class="posts">
        <TelegramPost
            v-for="post in posts"
            :key="post.id"
            :postId="`${post['chat.username']}/${post.id}`"
        />
      </ul>
    
    </div>
  </div>
</template>

<script>
  import postsData from '../assets/export';
  import TelegramPost from '../components/TelegramPost';

  export default {
    name: 'Home',
    components: {TelegramPost},
    data () {
      return {
        postCategories: {},
      };
    },

    created () {

    },

    mounted () {
      this.preparePostsData();
      console.log(this.postCategories);
    },

    methods: {
      preparePostsData () {
        postsData.forEach(post => {
          if (!this.postCategories[post.category]) this.postCategories[post.category] = [];
          post.message && this.postCategories[post.category].push(post);
        });
      },
    },
  };
</script>

<style lang="scss">
  .post-categories {
    &__item {
      margin-bottom: 45px;
    }
    
    &__title {
      margin-top: 0;
      margin-bottom: 0;
      font-size: 70px;
    }
    
    .posts {
      display: flex;
      overflow-x: scroll;
      padding-left: 0;
      list-style: none;
      
      .item {
        display: flex;
        align-items: center;
        justify-content: center;
        margin-right: 10px;
        min-width: 320px;
        min-height: 650px;
        position: relative;
        background-color: #15202b;
        border: 2px solid #364049;
        border-radius: 4px;
        
        &:after {
          content: "";
          display: block;
          position: absolute;
          left: 50%;
          top: 150px;
          width: 50px;
          height: 50px;
          margin-left: -25px;
          border-radius: 50%;
          border-color: white transparent;
          border-style: double;
          border-width: 6px;
          -webkit-animation: spinAnimation 1.2s linear infinite;
          animation: spinAnimation 1.2s linear infinite;
        }
        
        
        &[data-loaded] {
          background-color: transparent;
          border: none;
          align-items: flex-start;
  
          &:after {
            display: none;
          }
        }
      }
    }
  }
  
  @keyframes spinAnimation {
    from {
      transform: rotate(0deg)
    }
    to {
      transform: rotate(1turn)
    }
  }
</style>
