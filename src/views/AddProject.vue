<template>
  <form @submit.prevent="handleSubmit">
      <label for="title">Title</label>
      <input type="text" required v-model="title" />

      <label for="details">Details</label>
      <textarea required v-model="details"></textarea>

      <button type="">Add Project</button>
  </form>
</template>

<script>
export default {
    data() {
        return {
            title: '',
            details: '',
            uri: 'http://localhost:3000/projects/'
        }
    },

    methods: {
        handleSubmit() {
            let project = {
                title: this.title,
                details: this.details,
                complete: false
            }

            fetch(this.uri, {
                method: 'POST',
                headers: {'Content-Type': 'application/json'},
                body: JSON.stringify(project)
            })
            .then(response => {
                console.log(response);
                this.$router.push({ name: 'Home' });
            });



        }
    }
}
</script>

<style>
    form {
        background-color: #fff;
        padding: 20px;
        border-radius: 10px;
    }

    label {
        display: block;
        color: #bbb;
        text-transform: uppercase;
        font-size: 14px;
        font-weight: bold;
        letter-spacing: 1px;
        margin: 20px 0 10px 0;
    }

    input {
        padding: 10px;
        border: 0;
        border-bottom: 1px solid #ddd;
        width: 100%;
        box-sizing: border-box;
    }

    textarea {
        border: 1px solid #ddd;
        padding: 10px;
        width: 100%;
        box-sizing: border-box;
        height: 100px;
    }

    form button {
        margin: 20px auto 0;
        display: block;
        background-color: #00ce89;
        color: white;
        padding: 10px;
        border: 0;
        border-radius: 6px;
        font-size: 16px;
    }
</style>