<template>
  <div class="page-container">
    <md-app md-mode="fixed">
      <md-app-toolbar class="md-primary">
        <div class="md-toolbar-row">
          <div class="md-toolbar-section-start">
            <md-button class="md-icon-button" @click="menuVisible = !menuVisible">
              <md-icon>menu</md-icon>
            </md-button>
            <span class="md-title">{{nombre_app }}</span>
          </div>
          <div class="md-toolbar-section-end">
            <md-button class="md-icon-button">
              <md-icon>refresh</md-icon>
            </md-button>

            <md-menu md-direction="top-end">
              <md-button class="md-icon-button" md-menu-trigger><md-icon>more_vert</md-icon></md-button>
              <md-menu-content>
                <md-menu-item>
                  <md-icon>power_settings_new</md-icon>
                  <span class="md-list-item-text">Cerrar sesión</span>
                </md-menu-item>
              </md-menu-content>
            </md-menu>
          </div>

          <vue-fuse 
          :keys="keys" 
          :list="bikes" 
          :defaultAll="false" 
          :eventName="bikesChanged"
          class="fuse">
          </vue-fuse>
        </div>
      </md-app-toolbar>

      <md-app-drawer :md-active.sync="menuVisible">
        <md-toolbar class="md-transparent" md-elevation="0">Navigation</md-toolbar>

        <md-list>
          <md-list-item>
            <md-icon>people</md-icon>
            <span class="md-list-item-text">Personas</span>
            <md-badge class="md-primary" md-content="6" />
          </md-list-item>

          <md-list-item>
            <md-icon>power_settings_new</md-icon>
            <span class="md-list-item-text">Cerrar sesión</span>
          </md-list-item>

        </md-list>
      </md-app-drawer>

      <md-app-content>
        <card-persona></card-persona>
        <empty-persona></empty-persona>
        <agregar-persona></agregar-persona>
        <md-button class="md-fab md-primary md-fab-bottom-right" @click="activar_ventana_agregar()">
          <md-icon>add</md-icon>
        </md-button>

      </md-app-content>

      
    </md-app>
  </div>
</template>

<style lang="scss" scoped>
  .md-app {
    height: 100vh;
    border: 1px solid rgba(#000, .12);
  }

   // Demo purposes only
  .md-drawer {
    width: 230px;
    max-width: calc(100vw - 125px);
  }
  .md-fab{
    float: right;
  }

  .fuse{
    width: 100%;
    margin-left: 5px;
  }
</style>

<script>
export default {
  name: 'Reveal',
  data: () => ({
    menuVisible: false,
    nombre_app: 'Personas-Vue'
  }),
  methods:({
    activar_ventana_agregar(){
      EventBus.$emit('activar-ventana-agregar', true);
    }
  })
}
</script>