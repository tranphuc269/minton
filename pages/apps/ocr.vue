<template>
  <div id="app">
    <div class="container">
      <div class="image-list">
        <!-- Danh sách hình ảnh -->
        <div v-for="image in images" :key="image.id" class="image-item">
          <img :src="image.url" alt="Hình ảnh" ref="imageRef" @load="getImageSize" />
        </div>
      </div>
      <div class="input-panel">
        <!-- 10 ô input cố định -->
        <div
          class="input-item"
          v-for="i in 10"
          :key="i"
          @click="focusInput(i)"
          :class="{ 'focused': focusedInput === i }"
        >
          <input type="text" :placeholder="'Input ' + i" />
          <!-- Định nghĩa toạ độ bbox cho mỗi ô input -->
          <div v-if="focusedInput === i" class="bbox" :style="bboxStyle">
            <!-- Nội dung hình chữ nhật -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      focusedInput: null, // Lưu ô input đang được focus
      bbox: null, // Lưu toạ độ bbox (tương đối với ảnh)
      imageSize: { width: 600, height: 415 }, // Kích thước của ảnh
      images: [
        { id: 1, url: 'https://lsx.vn/wp-content/uploads/2022/04/t.jpg' },
        { id: 2, url: 'https://lsx.vn/wp-content/uploads/2022/04/t.jpg' },
        // Thêm nhiều hình ảnh khác ở đây
      ],
    };
  },
  computed: {
    bboxStyle() {
      if (this.bbox) {
        const [x1, y1, x2, y2] = this.bbox;
        const imageWidth = this.imageSize.width;
        const imageHeight = this.imageSize.height;

        // Tính toán vị trí tương đối của bbox trên ảnh
        const relativeX1 = x1 * imageWidth;
        const relativeY1 = y1 * imageHeight;
        const relativeX2 = x2 * imageWidth;
        const relativeY2 = y2 * imageHeight;

        return {
          position: 'absolute',
          top: `${relativeY1}px`, // Toạ độ y tương đối trên ảnh
          left: `${relativeX1}px`, // Toạ độ x tương đối trên ảnh
          width: `${relativeX2 - relativeX1}px`, // Chiều rộng bbox
          height: `${relativeY2 - relativeY1}px`, // Chiều cao bbox
          background_color : 'rgba(255, 0, 0, 0.2)' // Màu đỏ với opacity
        };
      } else {
        return {};
      }
    },
  },
  methods: {
    focusInput(inputIndex) {
      this.focusedInput = inputIndex;
      // Cập nhật toạ độ bbox tương ứng với ô input đã chọn
      switch (inputIndex) {
        case 1:
          this.bbox = [0.511, 0.041, 0.577, 0.076];
          break;
        case 2:
          this.bbox = [0.1, 0.1, 0.1, 0.1];
          break;
        // Thêm các trường hợp khác cho các ô input khác ở đây
        default:
          this.bbox = null;
      }

      // Focus vào ô input tương ứng
      this.$nextTick(() => {
        const inputRef = this.$el.querySelector(`.input-item:nth-child(${inputIndex}) input`);
        if (inputRef) {
          inputRef.focus();
        }
      });
    },
    getImageSize() {
      // Lấy kích thước của ảnh sau khi nó tải hoàn thành
      const imageRef = this.$refs.imageRef[0];
      if (imageRef) {
        this.imageSize.width = imageRef.width;
        this.imageSize.height = imageRef.height;
      }
    },
  },
};
</script>

<style scoped>
#app {
  display: flex;
  justify-content: center; /* Căn giữa theo chiều ngang */
  align-items: center; /* Căn giữa theo chiều dọc */
  height: 100vh; /* Để lấp đầy chiều cao màn hình */
}

.container {
  display: grid;
  grid-template-columns: 4fr 1fr; /* Phân chia thành 2 cột */
  grid-gap: 20px; /* Khoảng cách giữa cột */
  width: 80%; /* Chiếm 80% chiều rộng */
  max-width: 1000px; /* Giới hạn chiều rộng tối đa */
}

.image-list {
  display: flex;
  flex-direction: row; /* Sắp xếp các hình ảnh theo hàng ngang */
  flex-wrap: wrap; /* Cho phép các hình ảnh xuống dòng nếu không đủ không gian */
  padding: 10px; /* Khoảng cách ngoại vi */
  background-color: #f0f0f0; /* Màu nền của danh sách hình ảnh */
}

.image-item {
  /* Thêm kiểu dáng cho mỗi mục hình ảnh */
  margin: 10px;
}

.input-panel {
  /* không cần flex: 2; */
  padding: 10px; /* Khoảng cách ngoại vi */
  background-color: #f9f9f9; /* Màu nền của ô input */
}

.input-item {
  /* Thêm kiểu dáng cho mỗi ô input */
  margin: 10px;
}

.input-item.focused {
  position: relative; /* Đặt vị trí của ô input là relative */
}

.bbox {
  z-index: 2; /* Để bbox nổi lên trên ô input */
  opacity: 0.2; /* Độ mờ */
  background-color: #ff0000; /* Màu đỏ cho bbox */
}
</style>
