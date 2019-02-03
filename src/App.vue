<template>
<div id="app">
        {{ info }}
        <p>*************</p>
        {{ infos }}
        <h2 style="font-family:Fahkwang;">Upload a File - Vuejs API Call</h2>

        <form enctype="multipart/form-data">
            <div class="form-horizontal">
                <div class="form-group">
                    <p class="control-label col-md-2" style="font-family:Fahkwang;">Language</p>
                    <div class="col-md-10">
                        <select class="form-control" style="width:80%;" name="partitionkey">
                            <option value="English">English</option>
                            <option value="Spanish">Spanish</option>
                            <option value="French">French</option>
                            <option value="Chineese">Chineese</option>
                            <option value="Ngambaye">Ngambaye</option>
                        </select><br />
                    </div>
                </div>
                <div class="form-group">
                    <p class="control-label col-md-2" style="font-family:Fahkwang;">Book Title</p>
                    <div class="col-md-10">
                        <input type="text" name="title" class="form-control" style="width:80%;" maxlength="200">
                    </div>
                </div>
                <div class="form-group">
                    <p class="control-label col-md-2" style="font-family:Fahkwang;">Book Text</p>
                    <div class="col-md-10">
                        <textarea rows="5" class="form-control" style="width:80%;" name="body" maxlength="2000"></textarea>
                    </div>
                </div>
                <div class="form-group">
                    <p class="control-label col-md-2" style="font-family:Fahkwang;">Images</p>
                    <div class="col-md-10">
                        <input type="file" multiple="multiple" id="photoUrl" name="file" v-on:change="fileChange($event.target.files)" accept="application/vnd.msword, application/vnd.ms-excel, application/vnd.ms-powerpoint,
                text/plain, application/pdf, image/*">
                    </div>
                </div>
                <div class="form-group">
                    <p class="control-label col-md-2" style="font-family:Fahkwang;">Sounds</p>
                    <div class="col-md-10">
                        <input type="file" multiple="multiple" id="photoUrl" name="file" v-on:change="fileChange($event.target.files)" accept="application/vnd.msword, application/vnd.ms-excel, application/vnd.ms-powerpoint,
                text/plain, application/pdf, image/*">
                    </div>
                </div>
                <div class="form-group">
                    <p class="control-label col-md-2" style="font-family:Fahkwang;">Book Author</p>
                    <div class="col-md-10">
                        <input type="text" name="custom5" class="form-control" style="width:80%;" maxlength="100">
                    </div>
                </div>
                <div class="form-group">
                    <p class="control-label col-md-2" style="font-family:Fahkwang;">Tags</p>
                    <div class="col-md-10">
                        <input type="text" name="custom3" class="form-control" style="width:80%;" maxlength="500">
                    </div>
                </div>
            </div>
            <div class="form-group">
                <button type="button" v-on:click="upload()" class="btn btn-primary btn-lg" style="font-family:Fahkwang;width:25%;">Submit</button>
            </div>
        </form>
    </div>

</template>

<script>
    import axios from "axios";
    export default {
        name: 'app',
        data() {
            return {
                files: new FormData(),
                info: null,
                infos: null
            }
        },
        methods: {
            fileChange(fileList) {
                this.files.append("file", fileList[0], fileList[0].name);
            },
            upload() {
              axios({ method: "POST", "url": "https://merryfairytales.azurewebsites.net/api/getSAS", "data": {'container': 'getsastoken'}, "headers": {'Content-Type': 'application/json'}})
                .then(response => (this.info = response))
                .catch(error => (this.info = error))
              axios({ method: "POST", "url": "http://mekonecampusapi.azurewebsites.net/api/pictures", "data": this.files })
                .then(response => (this.infos = response))
                .catch(error => (this.infos = error));
            }
        }
    }
</script>

<style>
    #app {
    padding: 20px;
    }
</style>
