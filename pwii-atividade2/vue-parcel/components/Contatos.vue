<template>
  <div class="container">
    <h1>Agenda</h1>

    <hr />

    <template>

      <div class="form-contato form-group">
        <p>
          <input placeholder="Nome" type="text" name="nome" class="form-control"
                v-model="nome" />
        </p>
        <p>
          <input placeholder="Telefone" name="telefone" class="form-control"
                v-model="telefone" />
        </p>
        <button v-on:click="adicionarContato" type="submit" class="btn btn-primary">
          Salvar
        </button>
      </div>
    </template>
    

    <div class="list-group">
      <p v-if="numContatos <= 0">Adicione um contato na agenda...</p>
      <p v-else>Há {{ numContatos }} contatos na agenda.</p>

      <div class="list-group-item" v-for="(contato, index) in contatos" v-bind:key="index">
        <span class="nome_class">Nome: <strong>{{ contato.nome }}</strong></span>
        <p>
          <span class="telefone_class">
            Telefone: <strong>{{ contato.telefone }}</strong>
          </span>
        </p>
        <div>
          <a href="#" title="Excluir" v-on:click.prevent="excluirContato(index)">
            Excluir
          </a>
          <a href="#" title="Excluir" style="margin-left: 10px;"  v-on:click.prevent="editarContato(index)">
            Editar
          </a>
        </div>

      </div>
    </div>

    <hr />
  </div>
</template>

<script>

  export default {

    data() {
      return {
        contatos: [],
        nome: '',
        telefone: '',
        index: -1,
      }
    },
    methods: {
      adicionarContato() {
        
        if (this.nome.trim() === '' || this.telefone.trim() === '') {
          return;
        }
        if(this.index != -1){  
          this.contatos[this.index].nome = this.nome
          this.contatos[this.index].telefone = this.telefone
          this.index = -1
        } else {
          this.contatos.push({'nome': this.nome, 'telefone': this.telefone})
          this.nome = ""
          this.telefone = ""

        }
        
      },
      excluirContato(index) {
        this.contatos.splice(index, 1);
      },
      editarContato(index) {
          this.index = index
          this.nome = this.contatos[index].nome
          this.telefone = this.contatos[index].telefone
      }
    },
    computed: {
      numContatos() {
        return this.contatos.length;
      }
    },
    watch: {
      contatos(val) {
        console.log('val', val)
      }
    }
  }
</script>
