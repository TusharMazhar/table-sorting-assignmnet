<template>
<div>
    <v-app>
        <v-card width="50%" class="table">
            <v-data-table
                :headers="headers"
                :items="sampleData"
                :search="search"
                hide-default-footer
                disable-filtering
            ></v-data-table>
        </v-card>
    </v-app>
</div>
</template>

<script>

export default ({
    name:'Table',
    data () {
    return {
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
  
})
</script>
<style scoped>
 .table{
     margin: auto;
 }
</style>

