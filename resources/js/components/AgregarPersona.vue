<template>
  <div>
    <md-dialog :md-active.sync="showDialog" class="md-layout md-scrollbar">

        <form novalidate class="md-layout" @submit.prevent="validateUser">
            <md-card>
                <md-card-header>
                    <div class="md-title">{{nameDialog}}</div>
                </md-card-header>
                <md-card-content>
                    
                    <md-field :class="messageClass">
                        <label>Cedula</label>
                        <md-input v-model="cedula" type="number" required></md-input>
                        <span class="md-error">Debe ingresar su nombre</span>
                    </md-field>

                    <md-field :class="messageClass">
                        <label>Nombre</label>
                        <md-input v-model="nombre" required></md-input>
                        <span class="md-error">Debe ingresar su nombre</span>
                    </md-field>

                    <md-field :class="messageClass">
                        <label>Apellido</label>
                        <md-input v-model="apellido" required></md-input>
                        <span class="md-error">Debe ingresar su apellido</span>
                    </md-field>
                    
                    <md-field>
                        <label for="sexo">Sexo</label>
                        <md-select v-model="sexo" name="sexo" id="sexo">
                            <md-option v-for="sex in sexos" :value="sex.id" :key="sex.id">{{sex.valor}}</md-option>
                        </md-select>
                        {{sexo}}
                    </md-field>

                    <md-switch v-model="hasMessages">{{ !hasMessages ? 'Show' : 'Hide' }} Errors</md-switch>    

                </md-card-content>
                <!--<md-progress-bar md-mode="indeterminate" />-->
                <md-card-actions>
                    <md-button class="md-primary" @click="showDialog = false">{{nameCloseButton}}</md-button>
                    <md-button type="submit" class="md-primary" >{{nameSaveButton}}</md-button>
                </md-card-actions>
            </md-card>

            <md-snackbar :md-active.sync="userSaved">The user was saved with success!</md-snackbar>
        </form>

      

      <!--<md-dialog-actions>
        <md-button class="md-primary" @click="showDialog = false">Close</md-button>
        <md-button class="md-primary" @click="showDialog = false">Save</md-button>
      </md-dialog-actions>-->


    </md-dialog>

  </div>
</template>

<script>
  export default {
    name: 'DialogCustom',
    data: () => ({
      sexo:undefined,
      showDialog: false,
      nameDialog:"Nueva Persona",
      nameSaveButton:"Guardar",
      nameCloseButton:"Cerrar",
      noError: null,
      required: null,
      textarea: null,
      hasMessages: false,
      sexos:[
          {
              'id':1,
              'valor':'Masculino'
          },
          {
              'id':2,
              'valor':'Femenino'
          }
      ]
    }),
    computed: {
      messageClass () {
        return {
          'md-invalid': this.hasMessages
        }
      }
    },
    methods: () => ({
        
    }),mounted(){
        EventBus.$on('activar-ventana-agregar', data=>{
           this.showDialog = true;
        })
    }

  }
</script>

<style lang="scss" scoped>

    .md-card{
        width: 100%;
        margin-top:15px;
        padding: 5px;
    }
    .md-dialog {
        max-width: 768px;
    }

  
</style>