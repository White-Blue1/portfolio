<template>
  <div class="container-fluid bg-image" style="overflow: hidden;">
    <div class="row align-items-center" style="height: 100vh;">
      <div class="col-md-12 text-center">
        <div class="content">
          <h1>{{ name }}</h1>
          <div class="typing-effect">
            <span class="text">{{ typingText }}</span>
            <span class="cursor" :class="{ 'blink-animation': showCursor }"></span>
          </div>
          <div class="social-links">
            <GithubLogo></GithubLogo>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="js">
import GithubLogo from '~/components/GithubLogo.vue';

export default {
  components: {
    GithubLogo,
  },
}
</script>

<style scoped>
.container-fluid {
  padding: 0px;
}

.bg-image {
  background: #1d1d1d;
}

.content {
  text-align: center;
  color: #fff;
  position: relative;
  z-index: 1;
}

.typing-effect {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 1rem;
}

.text {
  font-size: 1.5em;
}

.cursor {
  display: inline-block;
  width: 0.5rem;
  height: 1.5rem;
  background-color: #fff;
  margin-left: 0.2rem;
}

.blink-animation {
  animation: blink 1s infinite;
}

.social-links {
  padding: 1rem;
  user-select: none;
}

@keyframes blink {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0;
  }
}

@keyframes erase {
  0% {
    width: 100%;
  }
  100% {
    width: 0;
  }
}
</style>

<script>
export default {
  head: {
    title: 'White Blue'
  },

  data() {
    return {
      name: 'White Blue/Luiz',
      typingText: '',
      showCursor: true,
      typingIndex: 0,
      typingPhrases: ['Sou um programador e cientista da computação', 'Desenvolvo em C, C++, Pawn, HTML/CSS, Vue.js, React, Next.js, Nuxt.js', 'Amo programação!', 'Only easy day was yesterday'],
      currentPhraseIndex: 0
    }
  },
  mounted() {
    this.startTypingEffect();
  },
  methods: {
    startTypingEffect() {
      const type = () => {
        const currentPhrase = this.typingPhrases[this.currentPhraseIndex];
        if (this.typingIndex < currentPhrase.length) {
          this.typingText += currentPhrase.charAt(this.typingIndex);
          this.typingIndex++;
          setTimeout(type, 40);
        } else {
          setTimeout(this.eraseText, 50);
        }
      };

      this.eraseText = () => {
        if (this.typingIndex > 0) {
          this.typingText = this.typingText.slice(0, -1);
          this.typingIndex--;
          setTimeout(this.eraseText, 50);
        } else {
          this.typingText = '';
          this.typingIndex = 0;
          this.currentPhraseIndex = (this.currentPhraseIndex + 1) % this.typingPhrases.length;
          setTimeout(type, 500);
        }
      };

      setInterval(() => {
        this.showCursor = !this.showCursor;
      }, 500);

      type();
    }
  }
}
</script>
