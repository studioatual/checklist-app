<template>
  <div class="checklist">
    <h2 class="checklist-title">{{ checklist.desc_checklist }}</h2>
    <div class="checklist-questions">
      <question v-for="(item, index) in checklist.questions" :key="index" :item="item" />
    </div>
    <button class="checklist-confirm">Confirmar</button>
  </div>
</template>

<script>
import Question from './components/Question';

export default {
  name: 'App',
  components: {
    Question,
  },
  data() {
    return {
      checklist: {
        cod_checklist: 1,
        desc_checklist: 'TESTE DE CHECKLIST',
        questions: [
          {
            cod_pergunta: 1,
            desc_pergunta: 'Qual módulo você mais usa?',
            cod_tipo: 1,
            desc_tipo: 'CAMPO DE RESPOSTA',
            posicao: 1,
            answer: null,
            answers: [],
            anexo: null,
            obs: 'Responda da forma mais adequada!',
            error: true,
            items: [],
          },
          {
            cod_pergunta: 2,
            desc_pergunta: 'Qual módulo você mais usa?',
            cod_tipo: 4,
            desc_tipo: 'CAMPO DE RESPOSTA',
            posicao: 2,
            answer: null,
            answers: [],
            anexo: null,
            obs: null,
            error: true,
            items: [],
          },
          {
            cod_pergunta: 3,
            desc_pergunta: 'Qual módulo você mais usa?',
            cod_tipo: 5,
            desc_tipo: 'DOCUMENTO',
            posicao: 3,
            answer: null,
            answers: [],
            anexo: null,
            obs: null,
            error: true,
            items: [],
          },
          {
            cod_pergunta: 4,
            desc_pergunta: 'Qual módulo você mais usa?',
            cod_tipo: 2,
            desc_tipo: 'MULTIPLAS RESPOSTAS',
            posicao: 4,
            answer: null,
            answers: [],
            anexo: null,
            obs: null,
            error: true,
            items: [
              {
                cod_item: 1,
                desc_item: 'Faturamento',
                obs: 'S',
                anexo: 'S',
                anexo_tipo: '0',
                posicao: 1,
              },
              {
                cod_item: 2,
                desc_item: 'Financeiro',
                obs: 'N',
                anexo: 'S',
                anexo_tipo: '1',
                posicao: 2,
              },
            ],
          },
          {
            cod_pergunta: 5,
            desc_pergunta: 'Qual módulo você mais usa?',
            cod_tipo: 3,
            desc_tipo: 'ALTERNATIVAS',
            posicao: 5,
            answer: null,
            answers: [],
            anexo: null,
            obs: null,
            error: true,
            items: [
              {
                cod_item: 1,
                desc_item: 'Faturamento',
                obs: 'S',
                anexo: 'N',
                anexo_tipo: '0',
                posicao: 1,
              },
              {
                cod_item: 2,
                desc_item: 'Financeiro',
                obs: 'N',
                anexo: 'S',
                anexo_tipo: '1',
                posicao: 2,
              },
            ],
          },
        ],
      },
    };
  },
};
</script>
