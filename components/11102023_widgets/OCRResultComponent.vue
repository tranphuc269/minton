<template>
  <div class="ocr-result-element" @click="onClickElement">
    <div>
      {{title}}
    </div>
    <div v-if="!isClicked">
      {{content}}
    </div>

    <div v-else>
      <input
        class="form-control"
        type="email"
        id="emailaddress"
        required
        placeholder="Enter your email"
        v-model="content"
      />
    </div>

  </div>
</template>

<script>
export default {
  name: "OCRResultComponent",
  data() {
    return {
      title: 'account_name',
      content: 'Công ty TNHH TM DV SX Hoàng Phú Anh',
      isClicked: false
    }
  },
  methods: {
    onClickElement(){
      this.isClicked = !this.isClicked;
    }
  }
}
</script>

<style scoped>

.ocr-result-element{
  margin: 0 4px;
  padding-left: 8px;
  border-left-style: solid;
  border-left-color: coral;
  border-left-width: 2px;
  cursor: pointer;
}
</style>
