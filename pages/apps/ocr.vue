<template>
  <div>
    <b-row no-gutters>
      <b-col cols="8">
        Em duc
      </b-col>

      <b-col cols="4" class="document-right-content">
        <div class="document-right-header justify-content-between">
          <span>1.QF - 34 TG Uy nhiem chi 2 lien.pdf</span>
          <span>...</span>
        </div>

        <b-tabs nav-class="nav-tabs nav-bordered">
          <b-tab title="Key-value" active>
            <OCRResultComponent></OCRResultComponent>
          </b-tab>
          <b-tab title="Table">

          </b-tab>
        </b-tabs>


      </b-col>
    </b-row>
  </div>
</template>

<script>
import {BTabs} from "bootstrap-vue";
import OCRResultComponent from "@/components/11102023_widgets/OCRResultComponent.vue";

export default {
  components: {OCRResultComponent, BTabs}

};
</script>

<style scoped>

.document-right-content{
  background-color: white;

  padding: 18px 0;
}
.document-right-header{
  display: inline-block;
}

</style>
