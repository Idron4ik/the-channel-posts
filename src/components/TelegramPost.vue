<template>
  <li ref="item" class="item"/>
</template>

<script>
  export default {
    name: 'TelegramPost',

    props: {
      postId: {
        type: String,
        require: true,
      },
    },

    mounted () {
      const script = document.createElement('script');
      script.setAttribute('async', true);
      script.setAttribute('data-telegram-post', this.postId);
      script.setAttribute('data-width', 10);
      script.setAttribute('data-userpic', false);
      script.setAttribute('data-color', 'CA9C0E');
      script.setAttribute('data-dark', 1);
      script.setAttribute('data-dark-color', 'F0B138');
      script.setAttribute('src', 'https://telegram.org/js/telegram-widget.js?15');

      const options = {
        threshold: 0.35,
      };

      const callback = entries => {
        const entry = entries[0];
        if (entry.isIntersecting) {
          if (!entry.target.hasAttribute('data-loaded')) {
            this.$refs['item'].appendChild(script);
            script.onload = () => {
              entry.target.setAttribute('data-loaded', true);
            };
          }
        }
      };

      const observer = new IntersectionObserver(callback, options);

      observer.observe(this.$refs['item']);
    },
  };
</script>
