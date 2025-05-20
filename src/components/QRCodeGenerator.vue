<template>
  <div class="qrcode-generator">
    <h2>QRCode 產生器</h2>
    <form @submit.prevent="generateQRCode">
      <input v-model="url" type="text" placeholder="請輸入網址" required />
      <button type="submit">產生 QRCode</button>
    </form>
    <div v-if="qrcodeDataUrl" class="qrcode-result">
      <img :src="qrcodeDataUrl" alt="QRCode 圖片" />
      <a :href="qrcodeDataUrl" download="qrcode.png">下載 QRCode</a>
    </div>
  </div>
</template>

<script>
import QRCode from 'qrcode';

export default {
  name: 'QRCodeGenerator',
  data() {
    return {
      url: '',
      qrcodeDataUrl: ''
    };
  },
  methods: {
    async generateQRCode() {
      try {
        this.qrcodeDataUrl = await QRCode.toDataURL(this.url);
      } catch (err) {
        alert('產生 QRCode 失敗，請確認網址格式正確');
      }
    }
  }
};
</script>

<style scoped>
.qrcode-generator {
  max-width: 400px;
  margin: 2rem auto;
  padding: 2rem;
  border: 1px solid #eee;
  border-radius: 8px;
  background: #fff;
  box-shadow: 0 2px 8px #eee;
}
.qrcode-generator input {
  width: 70%;
  padding: 0.5rem;
  margin-right: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.qrcode-generator button {
  padding: 0.5rem 1rem;
  border: none;
  background: #42b983;
  color: #fff;
  border-radius: 4px;
  cursor: pointer;
}
.qrcode-result {
  margin-top: 1.5rem;
  text-align: center;
}
.qrcode-result img {
  width: 200px;
  height: 200px;
}
.qrcode-result a {
  display: block;
  margin-top: 1rem;
  color: #42b983;
  text-decoration: underline;
}
</style>
