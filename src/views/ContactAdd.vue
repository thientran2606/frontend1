<template>
  <div class="page">
    <h4>Thêm mới Liên hệ</h4>
    <ContactForm :contact="{}" @submit:contact="createContact" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
  components: {
    ContactForm,
  },
  data() {
    return {
      message: "",
    };
  },
  methods: {
    async createContact(data) {
      try {
        await ContactService.create(data);
        alert("Liên hệ được thêm mới thành công.");
        this.$router.push({ name: "contactbook" });
      } catch (error) {
        console.error("Error creating contact:", error);
        this.message = "Đã xảy ra lỗi khi thêm liên hệ mới. Vui lòng thử lại.";
      }
    },
  },
};
</script>
