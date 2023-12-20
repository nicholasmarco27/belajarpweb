<template>
  <div class="registration-form-container">
    <h2 class="form-title">Form Registrasi</h2>
    <form @submit.prevent="submitForm" class="form">
      <div class="form-group">
        <label for="nama" class="form-label">Nama:</label>
        <input type="text" id="nama" v-model="Data.nama" required class="form-input" />
      </div>
      <div class="form-group">
        <label for="email" class="form-label">Email:</label>
        <input type="email" id="email" v-model="Data.email" required class="form-input" />
      </div>
      <div class="form-group">
        <label for="asal_sekolah" class="form-label">Asal Sekolah:</label>
        <input type="text" id="asal_sekolah" v-model="Data.asal_sekolah" required class="form-input" />
      </div>
      <div class="form-group">
        <label for="tanggal_pendaftaran" class="form-label">Tanggal Registrasi:</label>
        <input type="date" id="tanggal_pendaftaran" v-model="Data.tanggal_pendaftaran" required class="form-input" />
      </div>
      <button type="submit" class="submit-button">
        Register
      </button>
    </form>
  </div>
</template>



<script>
export default {
  data() {
    return {
      Data: {
        nama: "",
        email: "",
        asal_sekolah: "",
        tanggal_pendaftaran: "",
      },
    };
  },
  methods: {
    async submitForm() {
      try {
        const apiUrl = "http://localhost:8000/api/registrasi";

        const response = await fetch(apiUrl, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(this.Data),
        });

        const responseData = await response.json();

        console.log("Registration Data Successfully Submitted:", responseData);

        // Reset form after submission
        this.Data = {
          nama: "",
          email: "",
          asal_sekolah: "",
          tanggal_pendaftaran: "",
        };
        this.$router.push('/checkstatus');
      } catch (error) {
        console.error("An error occurred while submitting data:", error);
      }
    },
  },
};
</script>

<style scoped>
.registration-form-container {
  max-width: 400px;
  margin: 4rem auto;
  padding: 2rem;
  background-color: #FFF8DC;
  border-radius: 0.5rem;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.form-title {
  font-size: 1.5rem;
  text-align: center;
  margin-bottom: 1rem;
  color: #2b6cb0;
  font-weight: bold;
}

.form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 1rem;
}

.form-label {
  font-size: 0.875rem;
  margin-bottom: 0.25rem;
  color: #4a5568;
}

.form-input {
  padding: 0.5rem;
  border: 1px solid #cbd5e0;
  border-radius: 0.25rem;
  outline: none;
}

.submit-button {
  background-color: #008000;
  color: #fff;
  padding: 0.75rem;
  border: none;
  border-radius: 0.25rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.submit-button:hover {
  background-color: #2c5282;
}
</style>