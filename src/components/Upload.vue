<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-form ref="form">
          <v-file-input 
              label="Upload arquivo"
              v-model="file" 
              :rules="[v => !!v || 'Arquivo é obrigatório']"
              show-size 
              counter
              accept=".json"
              prepend-icon="mdi-file"
              @change="submidtForm"
          >
         
          </v-file-input>
      </v-form>
      </v-col>
      <v-col cols="12" md="12" xs="12" sm="12">
              <v-snackbar
                      v-model="snackbar"
                      :timeout="timeoutSnackbar"
                      top
                      :color="colorError"

              >
                  {{ textSnackbar }}

                  <template v-slot:action="{ attrs }">
                      <v-btn

                              v-bind="attrs"
                              @click="snackbar = false"
                              dark
                              text
                              small
                                  >
                          Fechar
                      </v-btn>
                  </template>
              </v-snackbar>
      </v-col>
      </v-row>
      <v-row>
        <v-col>
            <v-card>
        <v-toolbar
          color="red darken-2"
          dark
          
        >
          <v-toolbar-title>Resultado da Análise</v-toolbar-title>

          <v-spacer></v-spacer>

          <template v-slot:extension>
            <v-tabs
              v-model="tab"
              align-with-title
              centered
          >
              <v-tabs-slider color="red"></v-tabs-slider>
              <v-tab
                v-for="item in items"
                :key="item"
              >
                {{ item }}
              </v-tab>
            </v-tabs>
          </template>
        </v-toolbar>
        <v-tabs-items v-model="tab">
          <v-tab-item
      
          >
            <v-card flat>
              <v-card-text>
                <template>
                  <v-card>
                    <v-card-title>
                      <v-text-field
                        v-model="searchCandidato"
                        append-icon="mdi-magnify"
                        label="Search"
                        single-line
                
                      ></v-text-field>
                    </v-card-title>
                    <v-data-table
                      :headers="headersCandidato"
                      :items="dessertsCandidato"
                      :search="searchCandidato"
                    ></v-data-table>
                  </v-card>
                </template>
              </v-card-text>
            </v-card>
          </v-tab-item>
          <v-tab-item>
            <v-card flat>
              <v-card-text>
                <template>
                  <v-card>
                    <v-card-title>
                      <v-text-field
                        v-model="searchImcFaixa"
                        append-icon="mdi-magnify"
                        label="Search"
                        single-line
                      ></v-text-field>
                    </v-card-title>
                    <v-data-table
                      :headers="headersImcFaixa"
                      :items="dessertsImcFaixa"
                      :search="searchImcFaixa"
                    ></v-data-table>
                  </v-card>
                </template>
              </v-card-text>
            </v-card>
          </v-tab-item>
          <v-tab-item>
            <v-card flat>
              <v-card-text>
                <template>
                  <v-card>
                    <v-card-title>
                      <v-text-field
                        v-model="searchMediaIdade"
                        append-icon="mdi-magnify"
                        label="Search"
                        single-line
                      ></v-text-field>
                    </v-card-title>
                    <v-data-table
                      :headers="headersMediaIdade"
                      :items="dessertsMediaIdade"
                      :search="searchMediaIdade"
                    ></v-data-table>
                  </v-card>
                </template>
              </v-card-text>
            </v-card>
          </v-tab-item>
          <v-tab-item>
            <v-card flat>
              <v-card-text>
                <template>
                  <v-card>
                    <v-card-title>
                      <v-text-field
                        v-model="searchTotalObesos"
                        append-icon="mdi-magnify"
                        label="Search"
                        single-line
                      ></v-text-field>
                    </v-card-title>
                    <v-data-table
                      :headers="headersTotalObesos"
                      :items="dessertsTotalObesos"
                      :search="searchTotalObesos"
                    ></v-data-table>
                  </v-card>
                </template>
              </v-card-text>
            </v-card>
          </v-tab-item>
          <v-tab-item>
            <v-card flat>
              <v-card-text>
                <template>
                  <v-card>
                    <v-card-title>
                      <v-text-field
                        v-model="searchTotalDoadoresTipo"
                        append-icon="mdi-magnify"
                        label="Search"
                        single-line
                      ></v-text-field>
                    </v-card-title>
                    <v-data-table
                      :headers="headersTotalDoadoresTipo"
                      :items="dessertsTotalDoadoresTipo"
                      :search="searchTotalDoadoresTipo"
                    ></v-data-table>
                  </v-card>
                </template>
              </v-card-text>
            </v-card>
          </v-tab-item>
        </v-tabs-items>
      </v-card>
        </v-col>
      </v-row>
  </v-container>
</template>
<script>
  export default {
    name: 'Upload',
    data: () => ({
      file:null,
       tab: true,
        show:false,
        snackbar:false,
        textSnackbar:'',
        colorError:'error',
        timeoutSnackbar:5000,
        items: [
          'Candidatos por Estados', 'Média Imc por faixa',' Média idade tipo Sanguineo', '% Obesos Homem/Mulher', 'Doadores por Receptores',
        ],
        searchCandidato: '',
        headersCandidato: [
          {
            text: 'Estado',
            align: 'start',
            value: 'estado',
          },
          { text: 'Qtd', value: 'qtd' },

        ],
        dessertsCandidato: [],
       
        searchImcFaixa: '',
        headersImcFaixa: [
          {
            text: 'Faixa Inicio',
            align: 'start',
            value: 'faixaInicio',
          },
          { text: 'Faixa Fim', value: 'faixaFim' },
          { text: 'Média', value: 'mediaIcm' },

        ],
        dessertsImcFaixa: [],
        
        searchMediaIdade: '',
        headersMediaIdade: [
          {
            text: 'Tipo Sanguineo',
            align: 'start',
            value: 'tipoSanguineo',
          },
          { text: 'Média Idade', value: 'mediaIdade' },

        ],
        dessertsMediaIdade: [],
        searchTotalObesos: '',
        headersTotalObesos: [
          {
            text: 'Sexo',
            align: 'start',
            value: 'sexo',
          },
          { text: 'Percentual', value: 'percentual'},

        ],
        dessertsTotalObesos: [],
        searchTotalDoadoresTipo: '',
        headersTotalDoadoresTipo: [
          {
            text: 'Tipo',
            align: 'start',
            value: 'tipo',
          },
          { text: 'Quantidade', value: 'qtd'},

        ],
        dessertsTotalDoadoresTipo: [],
    }),
    methods:{
      async submidtForm() {
             
      if (this.$refs.form.validate()) {

            let formData = new FormData();
                formData.append('file', this.file);

                this.$http.post( 'http://localhost:8083/api/v1/upload',
                      formData,
                      {
                      headers: {
                          'Content-Type': 'multipart/form-data'
                      }
                    }
                  ).then(response=>{
                this.dessertsCandidato = response.data.candidatosEstado
                this.dessertsImcFaixa = response.data.imcFaixa
                this.dessertsMediaIdade = response.data.mediaIdade
                this.dessertsTotalObesos = response.data.totalObesos
                this.dessertsTotalDoadoresTipo = response.data.totalDoadoresTipo
                
                this.snackbar = true
                this.textSnackbar = 'Upload Realizado com Sucesso!'
                this.colorError ='success'
              })
              .catch(error=>{
                  this.snackbar = true
                  this.textSnackbar = 'Erro ao realizar Upload do arquivo'
                  this.colorError ='error'
              });


          }         

      }
            
    }
  }
</script>
