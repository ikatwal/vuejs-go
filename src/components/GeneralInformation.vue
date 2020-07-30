<template>
    <div class="information">
    <h4>
        General Information
    </h4>
    <p><label>MAC List Name:* </label>
    <input v-model="macListName" required="required" placeholder="Enter name" type="text">

    <!--<input type="text"></p>-->
    <p><label>Effective Date:* </label>
    <input v-model="effectiveDate" placeholder="Enter date" type="date">
    </p>
    <p><label>Termination Date: </label><input v-model="terminationDate" type="date"></p>
    <p><label for="checkbox">Publish to Portal:</label>
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
            <td>AWP Discount %</td>
            <td><input class="disc" v-model="awpGen" @input="onlyNumbers" type="text"></td>
            <td><input class="disc" v-model="awpSsg"  @input="onlyNumbers" type="text"></td>
            <td><input class="disc" v-model="awpSsb"  @input="onlyNumbers" type="text"></td>
            <td><input class="disc" v-model="awpSsbg"  @input="onlyNumbers" type="text"></td>
            <td><input class="disc" v-model="awpMsb"   @input="onlyNumbers" type="text"></td>
            <td><input class="disc" v-model="awpMsbg"  @input="onlyNumbers" type="text"></td>
        </tr>
        <tr>
            <td>WAC Discount %</td>
            <td><input class="disc" v-model="wacGen" @input="onlyNumbers" type="text"></td>
            <td><input class="disc" v-model="wacSsg" @input="onlyNumbers" type="text"></td>
            <td><input class="disc" v-model="wacSsb" @input="onlyNumbers" type="text"></td>
            <td><input class="disc" v-model="wacSsbg" @input="onlyNumbers" type="text"></td>
            <td><input class="disc" v-model="wacMsb" @input="onlyNumbers" type="text"></td>
            <td><input class="disc" v-model="wacMsbg" @input="onlyNumbers" type="text"></td>
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
      publishToPortal:false, baseMacList:"", clinicalDataSrc:"", status:"Draft",
      useNadac:false, nadacMarkup:0, orangeDrug:false, obsoleteDrug:false,
      eliminateSingleSrcBrand:false, setPricing:"", awpGen:0, awpSsb:0,
      awpMsbg:0, awpMsb:0, awpSsbg:0, awpSsg:0, wacGen:0, wacSsg:0, wacSsb:0,
      wacSsbg:0, wacMsb:0, wacMsbg:0
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
       this.awpGen = ''; 
       this.awpSsb = '';
       this.status = 'Draft';
       this.awpMsbg = ''; 
       this.awpMsb = ''; 
       this.awpSsbg = ''; 
       this.awpSsg = '';
       this.wacGen = '';
       this.wacSsg = '';
       this.wacSsb = '';
       this.wacSsbg = '';
       this.wacMsb = '';
       this.wacMsbg = '';
    },
    onlyNumbers: function() {
        if (!String(this.nadacMarkup).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
            this.nadacMarkup = '';
        }

        if (!String(this.awpGen).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
            this.awpGen = '';
        }

        if (!String(this.awpSsb).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
            this.awpSsb = '';
        }
                
        if (!String(this.awpMsbg).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
            this.awpMsbg = '';
        }

        if (!String(this.awpMsb).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
            this.awpMsb = '';
        }

        if (!String(this.awpSsbg).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
            this.awpSsbg = '';
        }

        if (!String(this.awpSsg).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
            this.awpSsg = '';
        }

         if (!String(this.wacGen).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
            this.wacGen = '';
        }

        if (!String(this.wacSsb).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
            this.wacSsb = '';
        }
                
        if (!String(this.wacMsbg).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
            this.wacMsbg = '';
        }

        if (!String(this.wacMsb).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
            this.wacMsb = '';
        }

        if (!String(this.wacSsbg).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
            this.wacSsbg = '';
        }

        if (!String(this.wacSsg).match(/^(\d{0,2}){1}([.]?\d{0,2})?$/)) {
            this.wacSsg = '';
        }
    },
    getData: function() {
        //Must validate MAC List name, Effective Date and Clinical Data Source
        if (this.macListName == '' || this.effectiveDate == '' || this.clinicalDataSrc == ''){
            return null;
        }
        var terminationDate = '';
        if (this.terminationDate == "") {
            terminationDate = "";
        } else {
            terminationDate = this.terminationDate + "T00:00:00Z";
        }
     
        
        return {
            "macListName": this.macListName, "effectiveDate": this.effectiveDate+"T00:00:00Z", 
            "terminationDate": terminationDate, "publishToPortal": this.publishToPortal,
            "baseMacList": this.baseMacList, "clinicalDataSrc": this.clinicalDataSrc, "useNadac": this.useNadac,
            "status": "Draft", "nadacMarkup": parseFloat(this.nadacMarkup), "orangeDrug": this.orangeDrug, 
            "obsoleteDrug": this.obsoleteDrug, "eliminateSingleSrcBrand": this.eliminateSingleSrcBrand, 
            "setPricingBy": this.setPricing, "awpDiscountGen":parseFloat(this.awpGen), 
            "awpDiscountMsb":parseFloat(this.awpMsb), "awpDiscountSsb":parseFloat(this.awpSsb),
            "awpDiscountMsbg":parseFloat(this.awpMsbg), "awpDiscountSsbg":parseFloat(this.awpSsbg),
            "awpDiscountSsg":parseFloat(this.awpSsg), "wacGen":parseFloat(this.wacGen), 
            "wacMsb":parseFloat(this.wacMsb), "wacSsb":parseFloat(this.wacSsb), 
            "wacMsbg":parseFloat(this.wacMsbg), "wacSsbg":parseFloat(this.wacSsbg), 
            "wacSsg":parseFloat(this.wacSsg)
        };
     
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

    label {
        padding-right: 5px; 
    }
    
    .disc {
        width: 100%; 
        box-sizing: border-box;
        -webkit-box-sizing:border-box;
        -moz-box-sizing: border-box;
    }
    p {
        padding-left: 10px;
        text-align: left;
    }

</style>