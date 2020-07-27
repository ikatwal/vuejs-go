<template>
    <div class="information">
        <h4>
            Alerts
        </h4>
        <p><label>Alert if AWP rises By %: </label><input v-model="awpRises" @input="onlyNumbers" type="text"></p>
        <p><label>Alert if AWP drops By %: </label><input v-model="awpDrops" @input="onlyNumbers" type="text"></p>
        <p><label>Alert if WAC rises By %: </label><input v-model="wacRises" @input="onlyNumbers" type="text"></p>
        <p><label>Alert if WAC drops By %: </label><input v-model="wacDrops" @input="onlyNumbers" type="text"></p>
        <p><label for="checkbox">New Drug to Market: </label>
            <input type="checkbox" id="checkbox" v-model="newDrug">
        </p>
        <p><label for="checkbox">Drug Type Change: </label>
            <input type="checkbox" id="checkbox2" v-model="drugType">
        </p>
        <p><label for="checkbox">Orange Book Code Change: </label>
            <input type="checkbox" id="checkbox3" v-model="orangeBook">
        </p>

        <p><label for="checkbox">Obsolete Drug: </label>
            <input type="checkbox" id="checkbox4" v-model="obsoleteDrug">
        </p>
    </div>
</template>

<script>


export default {
    name: "alerts",
    data: function() {
        return {
            awpRises:0,
            awpDrops:0,
            wacRises:0,
            wacDrops:0,
            newDrug:false,
            drugType:false,
            orangeBook:false,
            obsoleteDrug:false
        }
    },
    methods: {
        resetFields: function() {
            this.awpRises = 0;
            this.awpDrops = 0;
            this.wacRises = 0;
            this.wacDrops = 0;
            this.newDrug = '';
            this.drugType = '';
            this.orangeBook = '';
            this.obsoleteDrug = '';
        },
        onlyNumbers: function() {
            if (!String(this.awpRises).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
                    this.awpRises = '';
            }

            if (!String(this.awpDrops).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
                    this.awpDrops = '';
            }
            
            if (!String(this.wacRises).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
                    this.wacRises = '';
            }

            if (!String(this.wacDrops).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
                    this.wacDrops = '';
            }

        },
    
        getData: function() {
            return {
                "awpRise": parseFloat(this.awpRises), "awpDrop": parseFloat(this.awpDrops), 
                "wacRise": parseFloat(this.wacRises), "wacDrop": parseFloat(this.wacDrops),
                "newDrug": this.newDrug, "drugType": this.drugType, "orangeBook": this.orangeBook,
                "obsoleteDrug": this.obsoleteDrug
            }
        }
    }
}
</script>

<style scoped>

    .information {
        text-align: left;
        height: 100%;
        border: 1px black solid;
        margin: 5px 0 0 0;
    }

    p {
        padding-left: 10px;
        text-align: left;
    }

</style>