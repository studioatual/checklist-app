<template>
  <div class="checklist-answers-item">
    <div
      class="checklist-answers-item-checkbox"
      :class="{ selected: value.answer === item.cod_item }"
      @click="click"
    >
      <i v-if="value.answer === item.cod_item" class="fas fa-check-circle"></i>
      <i v-else class="far fa-circle"></i>
    </div>
    <div class="checklist-answers-item-content">
      <div
        class="checklist-answers-item-content-text"
        :class="{ selected: value.answer === item.cod_item }"
        @click="click"
      >{{ item.desc_item }}</div>
      <div v-if="value.answer === item.cod_item" class="checklist-answers-options">
        <answer-photo v-if="item.anexo === 'S' && item.anexo_tipo === '0'" v-model="value.anexo" />
        <answer-doc v-if="item.anexo === 'S' && item.anexo_tipo === '1'" v-model="value.anexo" />
        <answer-input v-model="value.obs" />
      </div>
    </div>
  </div>
</template>
<script>
import AnswerPhoto from '~/components/AnswerPhoto';
import AnswerDoc from '~/components/AnswerDoc';
import AnswerInput from '~/components/AnswerInput';

export default {
  name: 'AnswerRadio',
  props: ['item', 'value'],
  components: {
    AnswerPhoto,
    AnswerDoc,
    AnswerInput,
  },
  methods: {
    click() {
      this.$emit('input', {
        ...this.value,
        answer: this.item.cod_item,
      });
    },
  },
};
</script>
