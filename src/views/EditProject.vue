<template>
  <form @submit.prevent="EditProject">
      <label for="title">Title</label>
      <input type="text" required v-model="title" />

      <label for="details">Details</label>
      <textarea required v-model="details"></textarea>

      <button type="">Edit Project</button>
  </form>
</template>

<script>
export default {
    props: ['id'],
    data() {
        return {
            title: '',
            details: '',
            uri: 'http://localhost:3000/projects/' + this.id
        }
    },

    methods: {
        EditProject() {
            fetch(this.uri, {
                method: 'PATCH',
                headers: {'Content-Type': 'application/json'},
                body: JSON.stringify({title: this.title, details: this.details})
            })
            .then(rsp => this.$router.push({name: 'Home'}))
            .catch(error => console.log(error))
        }
    },

    mounted() {
        fetch(this.uri)
        .then(res => res.json())
        .then(response => {
            this.title = response.title;
            this.details = response.details
            console.log(response)
        })
        .catch(error => console.log(error))
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