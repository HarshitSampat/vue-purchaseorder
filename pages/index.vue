<script setup>
import info from '../data.json'
function totalExcludingTax() {
    let sum = 0
    info.Items.some((item) => {
        sum = sum + (item.UnitPrice * item.Quantity)
    })
    return sum
}
function getTotal() {
    let total = (totalExcludingTax() - 50) - (((totalExcludingTax() - 50) * info.TaxDetails.CGST.slice(0, 1) / 100) - ((totalExcludingTax() - 50) * info.TaxDetails.SGST.slice(0, 1) / 100)) + 0
    return total
}
</script>
<template>
    <div class="container m-auto">
        <div class="grid grid-cols-12">
            <div class="col-span-12 lg:col-span-10 lg:col-start-2 lg:col-span-6 lg:col-start-4 p-2">
                <h1 class="font-bold text-xl text-center">Purchase Order</h1>
                <div>
                    <img class="w-[100px]"
                        src="https://images.yourstory.com/cs/images/companies/105258679142755552588822938412209020921842n1-1656492402682.jpg?fm=auto&ar=1:1&mode=fill&fill=solid&fill-color=fff"
                        alt="img">
                </div>
                <div>
                    <div>
                        <table class="border border-black ml-auto text-sm">
                            <tr class="border border-black">
                                <th class="border border-black p-2">{{ Object.keys(info)[0] }}</th>
                                <td class="border border-black p-2">{{ Object.values(info)[0] }}</td>
                            </tr>
                            <tr class="border border-black">
                                <th class="border border-black p-2">{{ Object.keys(info)[1] }}</th>
                                <td class="border border-black p-2">{{ Object.values(info)[1] }}</td>
                            </tr>
                        </table>
                    </div>
                    <div class="sm:grid sm:grid-cols-2">
                        <BasicDetails :data="info.Vendor" heading="Vendor" />
                        <BasicDetails :data="info.ShipTo" heading="ShipTo" />
                    </div>
                    <div class="my-2 text-[14px]">
                        <table class="border border-black min-w-full">
                            <tr class="border border-black">
                                <th class="border border-black p-2">Delivery Method</th>
                                <th class="border border-black p-2">Payment Terms</th>
                                <th class="border border-black p-2">Delivery Date</th>
                                <th class="border border-black p-2">Against Quote No</th>
                            </tr>
                            <tr class="border border-black text-center">
                                <td class="border border-black p-2">{{ info.DeliveryMethod }}</td>
                                <td class="border border-black p-2">{{ info.PaymentTerms }}</td>
                                <td class="border border-black p-2">{{ info.DeliveryDate }}</td>
                                <td class="border border-black p-2">{{ info.AgainstQuoteNo }}</td>
                            </tr>
                        </table>
                    </div>
                    <div class="my-2 text-[13px]">
                        <table class="border border-black min-w-full">
                            <thead>
                                <tr class="border border-black">
                                    <th class="border border-black p-2" v-for="key in Object.keys(info.Items[0])">{{ key }}
                                    </th>
                                    <th class="border border-black p-2">Total(₹)</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr class="border border-black" v-for="(item, index) of info.Items">
                                    <td class="border border-black p-2 text-center" v-for="val in Object.values(item)">{{
                                        val }}
                                    </td>
                                    <td class="border border-black p-2 text-end">{{ (item.UnitPrice *
                                        item.Quantity).toFixed(2)
                                    }}
                                    </td>
                                </tr>
                                <tr v-if="(8 - info.Items.length > 0)" v-for="row in (8 - info.Items.length)">
                                    <td v-for="col in 5" class="border border-black p-2 text-center">
                                        &nbsp;
                                    </td>
                                </tr>
                                <tr>
                                    <td class="border border-black p-2">&nbsp;</td>
                                    <td class="border border-black p-2 font-medium text-center">Total Excl. Tax</td>
                                    <td class="border border-black p-2" colspan="2">&nbsp;</td>
                                    <td class="border border-black p-2 font-medium">₹{{ (totalExcludingTax()).toFixed(2) }}
                                    </td>
                                </tr>
                                <tr>
                                    <td class="border border-black p-2 text-sm" style="vertical-align: top;" colspan="2"
                                        rowspan="7">Note:</td>
                                    <td class="border border-black p-2" colspan="2">Discount</td>
                                    <td class="border border-black p-2 text-right">₹ 50</td>
                                </tr>
                                <tr>
                                    <td class="border border-black p-2" colspan="2">Other Costs</td>
                                    <td class="border border-black p-2  text-right">₹ 0</td>
                                </tr>
                                <tr>
                                    <td class="border border-black p-2" colspan="2">CGST</td>
                                    <td class="border border-black p-2 text-right">{{ info.TaxDetails.CGST }}</td>
                                </tr>
                                <tr>
                                    <td class="border border-black p-2" colspan="2">SGST</td>
                                    <td class="border border-black p-2  text-right">{{ info.TaxDetails.SGST }}</td>
                                </tr>
                                <tr>
                                    <td class="border border-black p-2 font-medium" colspan="2">Total</td>
                                    <td class="border border-black p-2  text-right">₹{{ getTotal().toFixed(2) }}</td>
                                </tr>
                                <tr>
                                    <td class="border border-black p-2 text-xs text-end" colspan="3" rowspan="2">Authorized
                                        Signature</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
</div></template>