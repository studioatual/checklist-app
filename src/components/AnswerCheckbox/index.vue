<template>
  <div class="checklist-answers-item">
    <div
      class="checklist-answers-item-checkbox"
      :class="{ selected: value.find((i) => i === item.cod_item) }"
      @click="click"
    >
      <i v-if="value.find((i) => i === item.cod_item)" class="fas fa-check-square"></i>
      <i v-else class="far fa-square"></i>
    </div>
    <div class="checklist-answers-item-content">
      <div
        class="checklist-answers-item-content-text"
        :class="{ selected: value.find((i) => i === item.cod_item) }"
        @click="click"
      >{{ item.desc_item }}</div>
      <div v-if="value.find((i) => i === item.cod_item)" class="checklist-answers-options">
        <answer-photo v-if="item.anexo === 'S' && item.anexo_tipo === '0'" />
        <answer-doc v-if="item.anexo === 'S' && item.anexo_tipo === '1'" />
        <answer-input v-if="item.obs === 'S'" />
      </div>
    </div>
  </div>
</template>
<script>
import AnswerPhoto from '~/components/AnswerPhoto';
import AnswerDoc from '~/components/AnswerDoc';
import AnswerInput from '~/components/AnswerInput';

export default {
  name: 'AnswerCheckbox',
  props: ['item', 'value'],
  components: {
    AnswerPhoto,
    AnswerDoc,
    AnswerInput,
  },
  methods: {
    click() {
      const values = Array.from(this.value);
      const index = values.findIndex((i) => i === this.item.cod_item);
      if (index < 0) {
        values.push(this.item.cod_item);
      } else {
        values.splice(index, 1);
      }
      this.$emit('input', values);
    },
  },
};
</script>
