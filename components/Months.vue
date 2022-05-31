<template>
    <v-simple-table class="months-in-year">
        <tr>
            <td class="mnths">January</td>
            <td class="mnths">February</td>
            <td class="mnths">March</td>
        </tr>
        <tr>
            <td class="mnths">April</td>
            <td class="mnths">May</td>
            <td class="mnths">June</td>
        </tr>
        <tr>
            <td class="mnths">July</td>
            <td class="mnths">August</td>
            <td class="mnths">September</td>
        </tr>
        <tr>
            <td class="mnths">October</td>
            <td class="mnths">November</td>
            <td class="mnths">December</td>
        </tr>  
    </v-simple-table>
</template>

<script>
    export default {
        name: 'Months',
    }
</script>

<style scoped>
.months-in-year { 
  font-size: 36px;
  width:100%;
}
.mnths {
    position:relative;
    text-align: left;
    width:300px;
}
.months-in-year > * {
  text-align: center;
  margin-right: 10px;
  height: 100px;
  padding-right: 5px;
  font-size: 28px;
  
}
</style>