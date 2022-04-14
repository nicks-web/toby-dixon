<template>
  <Layout>
    <div class="container">

      <div class="contact-header">
        <h3 class="contact-title">Contact</h3>
        <p>Leave me a note with any questions you might have, I'll get back to you as soon as possible.</p>
      </div>
   <form
     
     @submit.prevent="handleSubmit">
     <label v-for="(panelist, index) in panelists" :key="index">
       <input
         type="radio"
         name="panelist"
         @input="ev => form.askPerson = ev.target.value"
         :value="panelist"
         :checked="form.askPerson === panelist"
       />
       <span>{{ panelist }}</span>
     </label>
     
   </form>
 <script>
 import axios from "axios";
 export default {
   name: "QAForm",
   data () {
     return {
       form: {
         askPerson: ""
       }
     }
   },
   methods: {
     encode (data) {
       return Object.keys(data)
         .map(
           key => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`
         )
         .join("&");
     },
     handleSubmit () {
       const axiosConfig = {
         header: { "Content-Type": "application/x-www-form-urlencoded" }
       };
       axios.post(
         "/",
         this.encode({
           "form-name": "ask-question",
           ...this.form
         }),
         axiosConfig
       );
     }
   }
 }
 </script>



 <form name="contact" data-netlify-honeypot data-netlify="true">
 <input type="hidden" name="contact" value="contact" />
 <p>
     <label>Your Name: <input type="text" name="name" /></label>
  </p>
  <p>
    <label>Your Email: <input type="email" name="email" /></label>
  </p>
  <p>
    <label>Message: <textarea name="message"></textarea></label>
  </p>
  <p>
    <button class="button" type="submit">Send</button>
  </p>
</form>
    </div>
  </Layout>
</template>
<script>
export default {}
</script>

<style scoped>
.contact-header {
  padding: 2rem 0 4rem 0;
}
.contact-title {
  font-size: 2.2rem;
  margin: 0 0 4rem 0;
  padding: 0;
  font-family: Times New Roman, Georgia, serif;
}
.sender-info {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 2rem;
}
.sender-info > div {
  flex: 1;
  margin-right: 4rem;
}
.sender-info > div:last-of-type {
  margin: 0;
}
.hidden {
    display:none
}
input:focus,textarea:focus {
  border-color: var(--color-contrast-1);
}
input,textarea {
  background: transparent;
  border: 1px solid var(--color-base-1);
  outline: none;
  border-radius: 0.3rem;
  padding: 0.8rem 1rem;
  color: inherit;
  font-size: 1rem;
  width: 100%;
}
textarea {
  resize: none;
  height: 140px;
}
.button {
  color: var(--color-base);
  background: var(--color-contrast);
  outline: none;
  border: 0;
  font-size: 0.8rem;
  padding: 0.8rem 1.6rem;
  border-radius: 0.3rem;
  margin-top: 2rem;
  cursor: pointer;
  transition: opacity 0.25s ease;
  font-size: 500;
  letter-spacing: 0.035em;
}
.button:hover {
  opacity: 0.6;
}
.button:focus {
  border: 1px solid var(--color-base-1);
}
</style>

