<template>
    <div class="container">
        <h1>Comentários</h1>
        <hr />
        <form-to-do v-on:add-todo="addComment"></form-to-do>
        <div class="list-group">
            <p v-if="comments.length <= 0">Sem comentários...</p>
            <div class="list-group-item" v-for="(comment, index) in allComments" :key="comment.id">
                <span class="comment_author">Autor: <strong>{{ comment.name }}</strong></span
                >
                <p>{{ comment.message }}</p>
                <div>
                  <a href="#" title="Excluir" v-on:click.prevent="removeContents(index)"
                    >Excluir</a
                  >
                </div>
              </div>
            </div>
          </div>
</template>

<script>

import FormToDo from './FormToDo.vue';

// Implicitamente é gerado uma nova instância de new Vue({ })
export default {
  components: { FormToDo },

    // função data que retorna um objeto que tem a propriedade comments que é um array
    data() {
        return {
            comments: [{
               name: 'Tony Ramos',
               message: 'Lore Ipsun'
            }],
        };
    },

    methods: {
        addComment(comment) {
            this.comments.push(comment)
        },

        removeContents(index) {
            // remove o objeto através do indice
            this.comments.splice(index, 1);
        },
    },

    // computed esta mais relacionado com a interface e não é utilizado com a lógica do negócio.
    // no expemplo abaixo será exibido apenas na view, mas continua mando null para o bd
    computed: {
        allComments() {
            return this.comments.map((comment) => ({
                ...comment,
                name: comment.name === "" ? "Anônimo" : comment.name,
            }));
        },
    },
    
    // oberva qualquer alteração e pode ser aplicado mais alguma regra
    watch: {
        comments(val) {
            console.log("val", val);
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
