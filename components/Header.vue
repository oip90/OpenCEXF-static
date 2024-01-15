<template>
  <header id="header" class="header" :class="{scrolled: scrl}">
    <div class="content flex justify-between">
      <div class="header__logo">
        <nuxt-link :to="``" class="header__logo-link">
          <img :src="this.$config.axios.logo ? this.$config.axios.logo : '/img/logo_st.svg'" class="logo-desc" alt="logo" />
          <img :src="this.$config.axios.logo ? this.$config.axios.logo : '/img/logo_st-black.svg'" class="logo-mob" alt="logo" />
        </nuxt-link>
      </div>
      <div class="header__etc flex justify-between flex-no-wrap">
        <div class="header__language" @click.stop="toggleLangMenu">
          <div class="header__language-current">
            <span>
              {{lang}}
            </span>
            <img class="header__language-arr" src="/img/arr.svg" />
          </div>
          <ul :class="['navigation-language', { active: isMenuActivated.lang }]">
            <li class="navigation-language__item" v-for="item in ['en', 'ru']" :key="item">
              <a
                :class="[
                  'navigation-language__link',
                  { selected: lang === item },
                ]"
                @click.prevent="setLang(item)"
              >{{ item }}</a
              >
            </li>
          </ul>
        </div>
        <a href="/account/login" class="header-btn header-btn-signup">{{ $t('login') }}</a>
        <a href="/account/register" class="header-btn header-btn-register">{{ $t('Register') }}</a>
        <div class="header__menu" @click.stop="togglePageMenu">
          <div class="burger" :style="{ backgroundColor: scrl ? '#6352CD' : 'transparent' }">
            <img src="/img/burger.svg" />
            <!-- <span class="burger__text">{{ $t('menu') }}</span> -->
          </div>
          <ul class="navigation" :class="{ navigation__open: isMenuActivated.page }">
            <li class="navigation__item">
              <a href="/account/wallet" class="navigation__link">
                <img class="navigation__link__img" width="20" height="20" src="/public/img/menu/credit-card-alt.svg">
                {{ $t('wallet') }}
              </a>
            </li>
            <li class="navigation__item">
              <a
                href="/account/trade/BTC-USDT"
                class="navigation__link"
              >
                <img class="navigation__link__img" width="20" height="20" src="/public/img/menu/line-chart.svg">
                {{ $t('exchange') }}
              </a>
            </li>
            <li class="navigation__item">
              <a
                href="/account/quick-swap"
                class="navigation__link"
              >
                <img class="navigation__link__img" width="20" height="20" src="/public/img/menu/exchange.svg">
                {{ $t('quickBuySell') }}
              </a>
            </li>
            <li class="navigation__item">
              <a href="/account/fees" class="navigation__link">
                <img class="navigation__link__img" width="20" height="20" src="/public/img/menu/list-ul.svg">
                {{ $t('fees') }}
              </a>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {
      isMenuActivated: {
        lang: false,
        page: false
      },
      scrl: false
    }
  },
  computed: {
    lang() {
      return this.$store.getters.lang
    },
  },
  methods: {
    closeAll(){
      this.isMenuActivated.lang = false
      this.isMenuActivated.page = false
    } ,
    toggleLangMenu() {
      this.isMenuActivated.lang = !this.isMenuActivated.lang
      this.isMenuActivated.page = false
    },
    togglePageMenu() {
      this.isMenuActivated.page = !this.isMenuActivated.page
      this.isMenuActivated.lang = false
    },
    setLang(lang) {
      if (this.$route.params.lang !== lang) {
        this.$store.commit('SET_LANG', lang)
        const toLang = this.$route.params.lang
        const path = this.$nuxt.$route.path.replace(toLang, lang)
        this.$i18n.setLocale(lang)
        localStorage.setItem('lang', lang)
        this.$router.push({path: path})
      }
    },

    removeHandlers() {
      document.body.removeEventListener('click', this.closeAll)
    },

    addHandlers() {
      document.body.addEventListener('click', this.closeAll)
    },

    scrollAction() {
      const onScroll = () => {
        const scroll = document.documentElement.scrollTop
        if (scroll > 0) {
          this.scrl = true
        } else {
          this.scrl = false
        }
      }
      window.addEventListener('scroll', onScroll)
    }
  },

  beforeDestroy() {
    this.removeHandlers()
  },

  mounted() {
    this.addHandlers()
    this.scrollAction()
  },
}
</script>

<style scoped lang='scss'>
.header {
 /* padding-top: 37px; */
  padding-top: 0; // или уберите это свойство, если хотите удалить отступ
  height: 150px;
  position: absolute;
  top: 0;
  width: 100%;
  z-index: 2;
}
.header__etc {
  padding-top: 6px;
}
.navigation {
  display: none;
}
.header__menu {
  position: relative;
}
.navigation.navigation__open {
  position: absolute;
  top: 51px;
  left: -80px;
  display: block;
  width: 325%;
  background: #FFF;
  box-shadow: 0 0 2px 1px #00000040;
}
.navigation__item {
  color: #052E6B;
  padding: 12px 2px;
}
.navigation__link img {
  margin-left: 15px;
  margin-right: 20px;
}
.navigation__item a {
  display: flex;
  align-items: center;
  justify-content: flex-start;
}
.header__mob {
  display: none;
}
.navigation-language {
  display: none;
  position: absolute;
  top: 51px;
  left: 0;
  border: 1px solid #483D89;
  width: 100%;
  padding: 10px 20px;
  background: #6053C6;
}
.navigation-language__link {
  color: #052E6B;
  text-transform: capitalize;
  cursor: pointer;
  display: block;
  padding: 4px 0;
}
.navigation-language.active {
  display: block;
}
.header-btn {
  width: 96px;
  height: 46px;
/*  border: 1px solid #052E6B;  Цвет рамки */
/*  background-color: #052E6B;  Цвет фона */
  border-radius: 2px;
  text-align: center;
  color: #FFF; /* Общий цвет для обеих кнопок */
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: 10px;
  border-radius: 55px;
}
/* Цвет текста для кнопки "Login" */
.header-btn.header-btn-signup {
  border: none;
  color: #052E6B; 
}
.header-btn-register {
  /* Добавьте или обновите этот блок стилей для кнопки "Register" */
  background: #052E6B; /* Цвет фона для кнопки "Register" */
  color: #FFF; /* Замените "blue" на желаемый синий цвет */
}
.header__language {
  position: relative;
  display: flex !important;
}
.header__language-current {
  width: 102px;
  height: 46px;
  border: 1px solid #FFF;
  border-radius: 5px;
  text-align: center;
  color: #052E6B;
  display: none; //lang menu showing
  align-items: center;
  justify-content: space-between;
  padding: 0 20px;
}
.burger {
  margin-left: 5px;
  width: 35px;
  height: 46px;
  background: #6352CD;
  border-radius: 0px;
  color: #052E6B;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}
.burger__text {
  margin-left: 10px;
}
.header__language-current span {
  text-transform: uppercase;
}
.logo-mob {
  display: none;
}
.logo-desc {
  display: inline-block;
  padding-top: 6px;
  height: 53px;
  margin-left: 35px;
}
@media (max-width: 900px) {
  .header {
    height: 40px;
  }
  .logo-mob {
    display: inline-block;
  }
  .logo-desc {
    display: none;
  }
  .header {
    background: #FFF;
    padding-top: 8px;
  }
  .header__logo {
    width: 150px;
    height: 54px;
  }
  .header__language-current {
    color: #052E6B;
    height: 42px;
    border-radius: 0;
    position: relative;
    top: -1px;
    width: 70px;
  }
  .header-btn {
    color: #052E6B;
    height: 42px;
  /*  border-radius: 0; */ //заремарил
    position: relative;
    top: -1px;
    width: 70px;
    border-radius: 55px;
  }
  .burger {
    width: 40px;
    height: 40px;
    border-radius: 0;
    margin-right: -20px;
    margin-left: 0;
  }
  .navigation.navigation__open {
    position: absolute;
    top: 46px;
    left: 140px; /* ggggg */
    display: block;
    width: 223px;
  }
  .header-btn {
    color: #052E6B;
    margin-left: 0;
  }
  .header-btn-signup {
    border-radius: 5px; // Измените значение по своему вкусу
  }
  .header__etc {
    padding-top: 0;
    margin-top: -8px;
  }
  .burger__text {
    display: none;
  }
}
</style>
