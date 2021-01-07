<template>
    <v-container>
    <v-row justify="space-around">
      <v-card width="400">
        <v-img
          height="200px"
          src="https://atendimento.undb.edu.br/dbosco/acompanhamento/images/Marca-Dom-Bosco.png"
        >
        <!--https://www.undb.edu.br/hubfs/CAPA-SITE.jpg imagem UNDB-->
         
          <v-card-title class="white--text mt-8">
          
            
          </v-card-title>
        </v-img>
            
        <v-card-text>
          <div class="font-weight-bold ml-8 mb-2">
            {{messages[0].cliente}}
          </div>

          <v-timeline
            align-top
            dense
          >
            <v-timeline-item
              v-for="message in messages"
              :key="message.time"
              :color="message.color"
              small
            >
              <div>
                <div class="font-weight-normal">
                  Sua Senha: <strong> {{ message.senha }} {{ message.siglasenha }}</strong><br>Chegada:<strong> {{ message.time }} </strong>
                </div>
                <div>Você é o <strong>{{ message.message }}º</strong> na fila</div>
                <div>A estimativa de espera é: <strong>{{ message.estimativa }}</strong></div>
              </div>
            </v-timeline-item>
          </v-timeline>
        </v-card-text>
      </v-card>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Acomp',
  data: () => ({
    messages: [
      {
        cliente:'',
        senha: '',
        message: '',
        estimativa: '',
        siglasenha:'',
        time: '',
        color: 'deep-purple lighten-1',
      },
      
    ],
  }),
  mounted() {
    axios.get('https://atendimento.undb.edu.br/dbosco/public/api/filaAtendimento/1/REM/212/1').then((response) => {
      console.log(response.data)
      this.messages[0].cliente = response.data[0].nm_cli
      this.messages[0].time = response.data[0].dt_cheg
      this.messages[0].message = response.data[0].posicao
      this.messages[0].senha = response.data[0].num_senha
      this.messages[0].estimativa = response.data[0].estimativa_de_espera
      this.messages[0].siglasenha = response.data[0].sigla_senha
    })
  }
 
}
</script>
