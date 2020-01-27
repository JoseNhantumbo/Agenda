<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          icon="menu"
          aria-label="Menu"
          color ="black"
        />

      </q-toolbar>
      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class ="text-h3"> Agenda </div>
        <div class ="text-subtitle1">{{todaysDate}}</div>
      </div>
      <q-img
        src="statics/mountains.jpg"
        class="header-image absolute-top"/>
    </q-header>

    <<q-drawer
    v-model="leftDrawerOpen"
    show-if-above
    :width="250"
    :breakpoint="600"
  >
    <q-scroll-area style="height: calc(100%-198px); margin-top:198px; border-right:1px solid #ddd">
      <q-list padding>

        <q-item
          to="/"
          exact
        clickable
        v-ripple>
          <q-item-section avatar>
            <q-icon 
            name="list"
            />
          </q-item-section>

          <q-item-section>
            Realizar
          </q-item-section>
        </q-item>
        <q-item
          to="/help"
          exact
          clickable
          v-ripple>
          <q-item-section avatar>
            <q-icon name="help" />
          </q-item-section>

          <q-item-section
          color="black"
          >
            Ajuda
          </q-item-section>
        </q-item>

      </q-list>
    </q-scroll-area>

    <q-img class="absolute-top"   src="statics/mountains.jpg" style="height: 192px">
      <div class="absolute-bottom bg-transparent">
        <q-avatar size="56px" class="q-mb-sm">
          <img src="https://cdn.quasar.dev/img/boy-avatar.png">
        </q-avatar>
        <div class="text-weight-bold">José Nhantumbo</div>
        <div>nhantumbo2016@gmail.com</div>
      </div>
    </q-img>
  </q-drawer>


    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
  import { date } from 'quasar'
export default {
  name: 'MyLayout',

  data () {
    return {
      leftDrawerOpen: false
    }
  },
  computed :{
    todaysDate () {
      let timeStamp = Date.now()
      return  date.formatDate(timeStamp, 'dddd, D ' + " de " + '  MMMM', {
        days: ['Domingo', 'Segunda-feira','Terça-feira','Quarta-feira','Quinta-feira','Sexta-feira','Sábado'],
        daysShort: ['Dom', 'Sen','Ter','Qua','Quin','Sex','Sáb'],
        months: ['Janeiro', 'Fevereiro','Março' ,'Abril', 'Maio', 'Junho' ,'Julho' ,'Agosto', 'Setembro' ,'Outubro' ,'Novembro' ,'Dezembro'],
        monthsShort: ['Ian', 'Feb', ]
      })
    }
  }
}
</script>

<style lang ="scss">
  .header-image {
    height: 100%;
    z-index : -1;
    opacity: 0.3;
  }
</style>
