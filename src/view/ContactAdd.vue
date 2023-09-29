<template>
  <div class="page">
    <h4>Thêm Liên hệ</h4>
    <ContactFormAdd @submit:contact="createContact" />
    <div class="d-flex gap-3 mt-4 align-items-center">
      <p class="text-success m-0 fw-bold">{{ message }}</p>
      <router-link :to="{ name: 'contactbook' }">
        <span v-if="message" class="badge text-bg-primary"
          >Trở về trang chủ</span
        >
      </router-link>
    </div>
  </div>
</template>
<script>
import ContactFormAdd from "../components/ContactFormAdd.vue";
import ContactService from "../services/contact.service";
export default {
  components: {
    ContactFormAdd,
  },
  props: {
    id: { type: String, required: true },
  },
  data() {
    return {
      contact: null,
      message: "",
    };
  },
  methods: {
    async createContact(data) {
      try {
        await ContactService.create(data);
        this.message = "Đã tạo liên hệ mới thành công";
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
