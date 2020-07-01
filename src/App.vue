<template>
  <div id="app" data-server-rendered="true">
    <Hero :data="data.hero" />
    <Tiles :data="data.tile_section" />
    <LinkSection :data="data.link_section" />
    <Info :data="data.info_section" />
    <Collage />
    <Footer :data="data.footer" :language="currentLanguage"/>
    <Cookies :data="data.cookies" />
  </div>
</template>

<style lang="scss" scoped>
#app {
  overflow: hidden;
}
</style>

<script>
import pl_PL from '../public/content/pl_PL.json';
import en_EN from '../public/content/en_EN.json';
import Hero from './components/Hero'
import LinkSection from './components/LinkSection'
import Tiles from './components/Tiles'
const Info = () => import('./components/Info.vue');
const Collage = () => import('./components/Collage.vue');
const Footer = () => import('./components/Footer.vue');
const Cookies = () => import('./components/Cookies.vue');

export default {
  name: 'app',
  data() {
    return {
      data: pl_PL,
      currentLanguage: 'pl',
      languageList: {
        'pl': pl_PL,
        'en': en_EN
      }
    }
  },
  components: {
    Hero,
    Tiles,
    LinkSection,
    Info,
    Collage,
    Footer,
    Cookies
  },
  created() {
    this.setCurrentLanguage()
  },
  mounted() {
    this.orphanLetters()
  },
  methods: {
    setCurrentLanguage() {
      const param = window.location.search.substr(1);

      if (param) {
        const language = param.split('=')[1];

        if (language in this.languageList) {
          this.data = this.languageList[language];
          this.currentLanguage = language;
        } else {
          this.data = this.languageList['pl'];
          this.currentLanguage = 'pl';
        }
      
      } else {
        this.data = this.languageList['pl'];
        this.currentLanguage = 'pl';
      }
    },
    orphanLetters() {
      const paragraphs = document.querySelectorAll('.orphan-check')
      paragraphs.forEach(el => {
        let textReplace = el.innerHTML;
        const lettersToReplace = ['a', 'i', 'o', 'u', 'w', 'z', 'A', 'I', 'O', 'U', 'W', 'Z'];
        lettersToReplace.forEach(letter => {
          const textSplit = textReplace.split(' ' + letter + ' ');
          textReplace = textSplit.join(' ' + letter + '&nbsp;');
        })

        el.innerHTML = '';
        el.innerHTML = textReplace;
      });
    }
  }
}
</script>
