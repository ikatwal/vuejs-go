<template>
    <div class="information">
    <h4>
        General Information
    </h4>
    <p><label>MAC List Name:* </label>
    <input v-model="macListName" required="required" placeholder="Enter name" type="text">

    <!--<input type="text"></p>-->
    <p><label>Effective Date:* </label>
    <input v-model="effectiveDate" required="required" placeholder="Enter date" type="date">
    </p>
    <p><label>Termination Date: </label><input v-model="terminationDate" type="date"></p>
    <p><label for="checkbox">Publish to Portal: </label>
        <input v-model="publishToPortal" type="checkbox" id="checkbox">
    </p>
    <p><label>Base MAC List: </label>
        <select v-model="baseMacList">
            <option  value="">Please select one</option>
            <option>IL MAC</option>
            <option>MI MAC</option>
            <option>WA MAC</option>
        </select></p>
    <p><label>Clinical Data Source:* </label>
        <select v-model="clinicalDataSrc" required>
            <option disabled value="">Please select one</option>
            <option>Medispan</option>
            <option>FDB</option>
        </select></p>
    <label>Drug Type Discount</label>
    <table>
        <tr>
            <th>Discount Type</th>
            <th>Generic</th>
            <th>SSG</th>
            <th>SSB</th>
            <th>SSBG</th>
            <th>MSB</th>
            <th>MSBG</th>
        </tr>
        <tr>
            <td>AWP Discount</td>
            <td>85%</td>
            <td>80%</td>
            <td>75%</td>
            <td>70%</td>
            <td>70%</td>
            <td>70%</td>
        </tr>
        <tr>
            <td>WAC Discount</td>
            <td>80%</td>
            <td>75%</td>
            <td>70%</td>
            <td>80%</td>
            <td>80%</td>
            <td>80%</td>
        </tr>
    </table>
    <p><label for="checkbox">Use NADAC Pricing: </label>
    <input v-model="useNadac" type="checkbox" id="checkbox3">
    <p><label>Markup on NADAC: </label>
    <input v-model="nadacMarkup"  @input="onlyNumbers" placeholder="Enter markup" type="text">
    </p>
    <p><label for="checkbox">Include Non A/B Orange Rated Drugs: </label>
        <input v-model="orangeDrug" type="checkbox" id="checkbox3">
        
    </p>
    <p><label for="checkbox">Include Obsolete Drugs: </label>
        <input v-model="obsoleteDrug" type="checkbox" id="checkbox4">
    </p>
    <p><label for="checkbox">Eliminate Single Source Brands: </label>
        <input v-model="eliminateSingleSrcBrand" type="checkbox" id="checkbox5">
    </p>
    <p><label>Set Pricing By: </label>
        <select v-model="setPricing">
            <option disabled value="">Please select one</option>
            <option>GCN</option>
            <option>ETC</option>
            <option>NDC</option>
        </select>
    </p>
</div>
</template>

<script>
   



/* eslint-disable */

export default {
  name: 'general-information',
    data: function() {
    return {
      macListName:"", effectiveDate:"", terminationDate:"",
      publishToPortal:false, baseMacList:"", clinicalDataSrc:"",
      useNadac:false, nadacMarkup:0, orangeDrug:false, obsoleteDrug:false,
      eliminateSingleSrcBrand:false, setPricing:""
    }
  },
  methods: {
    resetFields: function() {
       this.macListName = '';
       this.effectiveDate = '';
       this.terminationDate = '';
       this.publishToPortal = '';
       this.baseMacList = '';
       this.clinicalDataSrc = '';
       this.nadacMarkup = 0;
       this.useNadac = '';
       this.orangeDrug = '';
       this.obsoleteDrug = '';
       this.eliminateSingleSrcBrand = '';
       this.setPricing = '';
    },
    onlyNumbers: function() {
      if (!String(this.nadacMarkup).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
            this.nadacMarkup = '';
      }
    },
    getData: function() {
        return {"macListName": this.macListName, "effectiveDate": this.effectiveDate, 
        "terminationDate": this.terminationDate, "publishToPortal": this.publishToPortal,
        "baseMacList": this.baseMacList, "clinicalDataSrc": this.clinicalDataSrc, "useNadac": this.useNadac,
        "nadacMarkup": parseFloat(this.nadacMarkup), "orangeDrug": this.orangeDrug, "obsoleteDrug": this.obsoleteDrug,
        "eliminateSingleSrcBrand": this.eliminateSingleSrcBrand, "setPricing": this.setPricing};
      /*eslint-disable*/
      console.log(data);
      /*eslint-enable*/


    }
  }
}
</script>

<style scoped>

    table, th, td {
        padding: 10px;
        text-align: left;
    }

    table {
        width: 98%;
        margin: 0 0 1% 1%;
        border: 1px solid black;
        border-collapse: collapse;
    }

    table td, table th {
        border-left: 1px solid #000;
        border-right: 1px solid #000;
    }

    table tr:first-child {
        background: gray;
    }

    table td:first-child {
        border-left: none;
    }

    table td:last-child {
        border-right: none;
    }

    tr:nth-child(even) {
        background: #d3d3d3;
    }

    tr:nth-child(odd) {
        background: white;
    }

    .information {
        height: 100%;
        border: 1px black solid;
        margin: 5px 0 0 0;
    }

    p {
        padding-left: 10px;
        text-align: left;
    }

</style>