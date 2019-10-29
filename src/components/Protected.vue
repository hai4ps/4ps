// src/components/Protected.vue
<template>
  <div>
    <h1>Only logged user can see this</h1>
    <div class="large-12 medium-12 small-12 cell">
      <label>File
        <input type="file" id="file" ref="file" v-on:change="handleFileUpload()"/>
      </label>
        <button v-on:click="submitFile()">Submit</button>
      <p>Ordered list:    {{response.data}}</p>
    </div>
  </div>
</template>

<script>
import { Auth } from 'aws-amplify'
import axios from 'axios'

export default {
  name: 'protected',
  data() {
    return {
      response: {}
    }
  },
  methods: {
      /*
        Submits the file to the server
      */
      submitFile(){
        /*
                Initialize the form data
            */
            let formData = new FormData();

            /*
                Add the form data we need to submit
            */
            formData.append('file', this.file);

        /*
          Make the request to the POST /single-file URL
        */
            axios.post( '/single-file',
                formData,
                {
                headers: {
                    'Content-Type': 'multipart/form-data'
                }
              }
            ).then(response => {
          console.log(response);
          this.response = response;
        })
        .catch(function(){
          console.log('FAILURE!!');
        });
      },

      /*
        Handles a change on the file upload
      */
      handleFileUpload(){
        this.file = this.$refs.file.files[0];
      }
    }
}
</script>

