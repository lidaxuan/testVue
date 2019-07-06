<template>
    <div>
        
        <form>
            <input type="text" value="" v-model="name" placeholder="请输入用户名">
            <input type="text" value="" v-model="age" placeholder="请输入年龄">
            <input type="file" @change="getFile($event)">
            <button @click="submitForm($event)">提交</button>
        </form>
    </div>
</template>

<script>
    export default {
        data: {
          name: '',
          age: '',
          file: ''
        },
        methods: {
          getFile(event) {
            this.file = event.target.files[0];
            console.log(this.file);
          },
          submitForm(event) {
            event.preventDefault();
            let formData = new FormData();
            formData.append('name', this.name);
            formData.append('age', this.age);
            formData.append('file', this.file);
 
            let config = {
              headers: {
                'Content-Type': 'multipart/form-data'
              }
            }
 
            this.$http.post('https://nbrecsys.4paradigm.com/action/api/log', formData, config).then(function (response) {
              if (response.status === 200) {
                console.log(response.data);
              }
            })
          }
        }
    }
</script>

<style>

</style>
