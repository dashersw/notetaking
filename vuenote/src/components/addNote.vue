<template lang="html">
  <div class="section">
    <h2 class="title is-2"> {{ addTitle }} </h2>
    <noteForm :is-edit="false" />
  </div>
</template>
<script>
import axios from "axios";
import HTTP from "../main.js";
import note from "@/components/note.vue";
import search from "@/components/search.vue";
import noteForm from "@/components/noteForm.vue";
window.axios = axios;
export default {
    components: {
        note,
        search,
        noteForm
    },
    data() {
        return {
            posts: [],
            errors: [],
            addTitle: "Add a Note"
        };
    },
    // Fetches posts when the component is created.
    created() {
        axios.get("http://localhost:3030/note")
            .then(response => {
                // JSON responses are automatically parsed.
                this.posts = response.data;
            })
            .catch(e => {
                this.errors.push(e);
            });

    // async / await version (created() becomes async created())
    //
    // try {
    //   const response = await axios.get(`http://jsonplaceholder.typicode.com/posts`)
    //   this.posts = response.data
    // } catch (e) {
    //   this.errors.push(e)
    // }
    }
};
</script>


