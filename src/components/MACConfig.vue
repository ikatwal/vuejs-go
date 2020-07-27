<template>
    <div id="mac-config">
        <p class="config-title">MAC Config</p>
        <div class="dashboard">
            <span class="dropdown">
            <label for="mac-list">MAC List: </label>
            <select name="mac-list" id="mac-list">
                <optgroup label="mac-list-titles">
                    <option value="MRx-MAC-List">MRx MI MAC-List</option>
                </optgroup>
            </select>
            </span>
            <span>
                <b-button @click="created = !created" :disabled="!created">Create New MAC List</b-button>
                <span class="created-by">Created By: EMartina</span>
                <span class="created-date">Created Date: 4/1/2020</span>
                <span class="status">Status: Approved</span>
            </span>
            <!-- other components -->
            <div>
                <table>
                    <tr>
                        <td class="tab">General Information</td>
                        <td class="tab">Pricing Configuration</td>
                    </tr>
                </table>
            </div>
            <div class='row'>
                <div class='column'>
                    <general-information ref="generalInformation" class="DTB"></general-information>
                    <!--                    <drug-type-breakdown class="DTB"></drug-type-breakdown>-->
                    <!--                    <clients-assigned class="DTB"></clients-assigned>-->
                    <!--                    <pharmacy-relation class="DTB"></pharmacy-relation>-->
                    <!--                    <top-ten-label class="DTB"></top-ten-label>-->
                </div>
                <div class="column">
                    <alerts ref="alerts" class="DTB"></alerts>
                    <!--                    <DOS-filter class="DTB"></DOS-filter>-->
                    <!--                    <historic-trends class="DTB"></historic-trends>-->
                </div>
            </div>
            <div class='row float-right'>
                <b-button class="margin-button" variant="primary" :disabled="isCreated()==true" v-on:click="save()">Save</b-button>  

                <b-button class="margin-button" variant="danger" @click="reset()">Cancel</b-button>  
            </div>
        </div>
    </div>
</template>

<script>
    import GeneralInformation from "./GeneralInformation";
    import Alerts from "./Alerts";
    import axios from 'axios';

    export default {
        name: "mac-config",
        data: function() {
            return {
                 created: true
            }
        },
        methods: {
            reset() {
                if(!this.created) {
                    this.created = !this.created
                }
                this.$refs.generalInformation.resetFields();
                this.$refs.alerts.resetFields();
            },
            isCreated(){
                return this.created;
            },
            save() {
                var obj1 = this.$refs.generalInformation.getData();
                var obj2 = this.$refs.alerts.getData()
                for (var key in obj2) {
                    obj1[key] = obj2[key]
                }

                var data = JSON.stringify(obj1);
                axios({ method: "POST", url: process.env.VUE_APP_BASE_URL, data: data, headers: {"content-type": "text/plain" } }).then(response => {
                    console.log(response)
                }).catch(error => {
                    console.error(error)
                });

            }
        },
        components: {
            GeneralInformation,
            Alerts
        }
    }
</script>

<style scoped>

    #mac-config {
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    .DTB {
        width: 100%;
    }

    .created-by, .created-date, .status {
        padding: 0 10px 0 10px;
    }

    .dropdown {
        float: left;
        padding-left: 10px;
    }

    .config-title {
        text-align: left;
    }

    .dashboard {
        border: 1px black solid;
        padding: 25px;
    }

    .row {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        width: 100%;
        margin: 10px;
    }

    .column {
        padding: 0 10px 10px 0;
        display: flex;
        flex-direction: column;
        flex-basis: 100%;
        flex: 1;
    }


    .tab {
        border-top: 1px solid black;
        border-left: 1px solid black;
        border-right: 1px solid black;
    }

    .float-right {
        flex-direction: row-reverse;

    }

    .margin-button {
        margin: 0 10px 0 10px;
    }

   

</style>