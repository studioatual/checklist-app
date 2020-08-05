<template>
  <div class="checklist-questions-item">
    <div class="checklist-questions-item-number">{{ item.posicao }}</div>
    <div class="checklist-questions-item-content">
      <h3 class="checklist-questions-item-title">{{ item.desc_pergunta }}</h3>
      <span v-if="item.obs" class="checklist-questions-item-obs">{{ item.obs }}</span>
      <div class="checklist-answers-options">
        <answer-photo v-if="item.cod_tipo === 4 || item.cod_tipo === 6" v-model="item.anexo" />
        <answer-doc v-if="item.cod_tipo === 5 || item.cod_tipo === 7" v-model="item.anexo" />
        <answer-input
          v-if="item.cod_tipo === 1 || item.cod_tipo === 6 || item.cod_tipo === 7"
          v-model="item.answer"
        />
      </div>
      <div v-if="item.cod_tipo === 2" class="checklist-answers">
        <answer-checkbox
          v-for="(answer, index) in item.items"
          :key="`checkbox_${index}`"
          :item="answer"
          v-model="item.answers"
        />
      </div>
      <div v-if="item.cod_tipo === 3" class="checklist-answers">
        <answer-radio
          v-for="(answer, index) in item.items"
          :key="`radio_${index}`"
          :item="answer"
          v-model="item"
        />
      </div>
    </div>
  </div>
</template>
<script>
import AnswerCheckbox from '~/components/AnswerCheckbox';
import AnswerRadio from '~/components/AnswerRadio';
import AnswerPhoto from '~/components/AnswerPhoto';
import AnswerDoc from '~/components/AnswerDoc';
import AnswerInput from '~/components/AnswerInput';

export default {
  name: 'Question',
  props: ['item'],
  components: {
    AnswerCheckbox,
    AnswerRadio,
    AnswerPhoto,
    AnswerDoc,
    AnswerInput,
  },
};
</script>
