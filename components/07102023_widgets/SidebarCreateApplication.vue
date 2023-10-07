<template>
  <div>
    <b-sidebar
      id="sidebar-backdrop"
      class="align-items-start"
      title="Tạo ứng dụng"
      no-close-on-backdrop="no-close-on-backdrop"
      bg-variant="white"
      backdrop
      right
      shadow
      :width="'640px'"
    >
      <template #footer="{ hide }">
        <div class="d-flextext-light align-items-center text-left pb-3">
          <b-button size="sm" @click="onNextStep">Tiếp tục</b-button>
          <b-button size="sm" v-b-toggle.sidebar-backdrop>Đóng</b-button>

        </div>
      </template>
      <b-form-group label-for="backdrop-variant">
        <div class="text-left application-form-step">
          <div class="application-form-step-0 "  v-if="step===0">
            <p>1. Thong tin ung dung</p>
            <div class="form-group">
              <label>
                Tên ứng dụng
                <span class="text-danger">*</span>
              </label>
              <input  type="email" name="email" class="form-control" placeholder="Tên ứng dụng" />
            </div>
            <div class="form-group">
              <label>
                Mô tả
                <span class="text-danger">*</span>
              </label>
              <textarea  type="email" name="email" class="form-control" placeholder="Nhập mô tả" />
            </div>
          </div>
          <div class="application-form-step-1 "  v-if="step===1">
            <p>2. Thong tin loại tài liệu cần xử lý</p>
            <div class="form-group">
              <input  type="email" name="email" class="form-control" placeholder="Tim kiem loai ung dung" />
            </div>
            <b-tabs content-class>
              <b-tab title="Home" active>
                <b-form-radio-group>
                  <b-table :items="items" :fields="fields" hover>
                    <!-- Custom Checkbox Slot -->
                    <template #cell(checkbox)="data">
                      <b-form-radio v-model="data.item.selected"></b-form-radio>
                    </template>

                    <!-- Custom Button Slot -->
                    <template #cell(actions)="data">
                      <b-button @click="handleButtonClick(data.item)" variant="primary">
                        Action
                      </b-button>
                    </template>
                  </b-table>
                </b-form-radio-group>
              </b-tab>
              <b-tab title="Profile">

              </b-tab>
              <b-tab title="Messages">

              </b-tab>
              <b-tab title="Settings">
              </b-tab>
            </b-tabs>
          </div>
        </div>
      </b-form-group>
    </b-sidebar>
  </div>
</template>

<script>
import {BSidebar} from "bootstrap-vue";

export default {
  name: "SidebarCreateApplication",
  components: {BSidebar},
  data() {
    return {
      step: 0,
      items: [
        { id: 1, name: "Item 1", selected: false },
        { id: 2, name: "Item 2", selected: false },
        { id: 3, name: "Item 3", selected: false }
      ],
      fields: [
        { key: "checkbox", label: "Select", sortable: false },
        { key: "id", label: "ID" },
        { key: "name", label: "Name" },
        { key: "actions", label: "Actions", sortable: false }
      ]
    }
  },
  methods: {
    createApplication() {
      /// post data
      /// callback function (aftercreated)
      /// close sidebar
      this.$emit('init')
    },

    onNextStep(){
      if(this.step === 0){
        this.step ++
      }else{
        // post data
        this.createApplication()
      }
    }
  }
}
</script>

<style scoped>

.application-form-step {
  padding: 20px 40px;
  width: 640px;
}

.d-flextext-light{
  padding: 20px 40px;
}

</style>
