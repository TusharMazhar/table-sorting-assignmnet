<template>
<div>
    <v-app>
        <v-card width="50%" class="table">
            <v-data-table
                id="exportable_table"
                :headers="headers"
                :items="sampleData"
                hide-default-footer
                disable-filtering
            ></v-data-table>
            <button @click="exportExcel('xlsx')" class="btn">Export Excel</button>
            <button @click="pdfDownload()" class="btn">Pdf Download</button>
            <button @click="pdfSave()" class="btn">Pdf Save</button>
        </v-card>
    </v-app>

</div>
</template>

<script>

import * as XLSX from 'xlsx/xlsx.mjs'
import jsPDF from 'jspdf'
import 'jspdf-autotable'

export default ({
    name:'Table',
    data () {
    return {
      head:[],
      body:[],
      headers: [
        { text: 'Book ID',value: 'Book_ID',},
        { text: 'Book Name', value: 'Book_Name' },
        { text: 'Category', value: 'Category' },
        { text: 'Price', value: 'Price' },

      ],
      sampleData: [
        {
            'Book_ID': '1', 
            'Book_Name': 'Challenging Times',
            'Category': 'Business',
            'Price': '125.60'
        },
        {
            'Book_ID': '2', 
            'Book_Name': 'Learning JavaScript',
            'Category': 'Programming', 
            'Price': '56.00'
        },
        {
            'Book_ID': '3', 
            'Book_Name': 'Popular Science',
            'Category': 'Science', 
            'Price': '210.40'
        }

   
      ],
    }
  },
  methods:{
       exportExcel(type, fn, dl) {
              var elt = document.getElementById('exportable_table')
              var wb = XLSX.utils.table_to_book(elt, { sheet: "sheet Js" });
              return dl
                ? XLSX.write(wb, { bookType: type, bookSST: true, type: "base64" })
                : XLSX.writeFile(
                    wb,(fn || "Table.") + (type || "xlsx")
                  );
          },
          pdfDownload(){
              let dataArr = []
              let arr = []
              this.head = []
              const doc = new jsPDF()
              this.headers.forEach(head=>{
                  arr.push(head.text)
                }
              )
              this.head.push(arr)

              this.body = Object.values(this.sampleData)
              this.body.forEach(item=>{
                  console.log(item)
                  dataArr.push(Object.values(item))
              })
              doc.autoTable({
                head: this.head,
                body: dataArr,
                })

                doc.save('table.pdf')

          },

          pdfSave(){
             window.print()
          }

  }
  
})
</script>
<style scoped>
 .table{
     margin: auto;
 }
 .btn{
     background-color: blue;
     color:white;
     padding: 10px;
     margin:10px
 }
</style>

