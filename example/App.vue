<template>
  <main class="app">
    <a
      :href="$options.repository"
      class="github-corner"
      aria-label="View source on GitHub"
    >
      <svg
        width="80"
        height="80"
        viewBox="0 0 250 250"
        style="fill:#151513; color:#fff; position: absolute; top: 0; border: 0; right: 0;"
        aria-hidden="true"
      >
        <path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z" /><path
          d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2"
          fill="currentColor"
          style="transform-origin: 130px 106px;"
          class="octo-arm"
        /><path
          d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z"
          fill="currentColor"
          class="octo-body"
        />
      </svg>
    </a>

    <header class="logo">
      <img
        :src="logo"
        alt="Talquei"
      >
    </header>

    <section class="content">
      <EditorWindow
        :height="height"
        title="~/Projects/app/index.js"
        class="editor"
      >
        <!-- eslint-disable-next-line vue/no-v-html -->
        <pre><code v-html="code" /></pre>
      </EditorWindow>

      <Talquei
        class="bot"
        :style="{ height: `${height}px` }"
      >
        <TalqueiMessage
          v-model="name"
          :input="{ tag: 'text', placeholder: 'Enter your name' }"
          text="Hi there! What's your name?"
        />
        <TalqueiMessage
          :text="`My name is ${name}`"
          :is-user="true"
        />
        <TalqueiMessage
          v-model="occupation"
          :text="`Great to meet you, ${name}! I'm a web form, what do you do?`"
          :input="{ tag: 'select', options: { design: 'Design', dev: 'Developer', other: 'Other' } }"
        />
        <TalqueiMessage
          :text="occupation"
          :is-user="true"
        />
        <TalqueiMessage
          text="This plugin can help you build webforms looking like a conversation. If you find this useful, please star us on GitHub!"
        >
          <div class="text-center">
            <a
              :href="$options.repository"
              alt="Open Github"
            >
              Open Github ⭐
            </a>
          </div>
        </TalqueiMessage>
      </Talquei>
    </section>
  </main>
</template>

<script>
import { EditorWindow } from 'vue-windows'
import hljs from 'highlight.js/lib/highlight'
import logoImage from './logo.png'

hljs.registerLanguage('javascript', require('highlight.js/lib/languages/javascript'))

export default {
  repository: 'https://github.com/luciorubeens/talquei',

  components: {
    EditorWindow,
  },

  data: () => ({
    height: 350,
    name: '',
    occupation: '',
    code: hljs.highlight('javascript', `import {Talquei, TalqueiMessage} from 'vue-talquei'

new Vue({
  el: '#app',
  render(h) {
    return h(Talquei, [
      h(TalqueiMessage, {props: {text: 'Hello!'}})
    ])
  }
})

// see more examples
// https://github.com/luciorubeens/talquei#usage
`).value,
  }),

  computed: {
    logo () {
      return logoImage
    },
  },
}
</script>

<style src="vue-windows/dist/vue-windows.css"></style>
<style src="highlight.js/styles/androidstudio.css"></style>
<style>
body {
  background-color: #16a085;
  background-image: linear-gradient(300deg, #16a085 0%, #1abc9c 100%);
  margin: 0;
  font-family: 'system-ui', '-apple-system', 'BlinkMacSystemFont', 'Segoe UI', 'Helvetica Neue', sans-serif;
}

a {
  text-decoration: none;
  color: #3490dc;
}

a:hover {
  text-decoration: underline;
}

.text-center {
  text-align: center;
}

.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.logo {
  margin-bottom: 2rem;
  text-align: center;
}

.logo img {
  width: 80%;
}

.content {
  display: flex;
  align-items: stretch;
}

.bot {
  width: 350px;
}

.social {
  color: #ffffff;
}
</style>
