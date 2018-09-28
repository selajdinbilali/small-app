<template>
  <v-container fluid>
    <v-slide-y-transition mode="out-in">
      <v-layout column align-center>

  <v-data-table
    :headers="headers"
    :items="info"
		:pagination.sync="pagination"
    hide-actions
    class="elevation-1"
  >
    <template slot="items" slot-scope="props">
      <td class="text-xs-right">{{ props.item.name }}</td>


		</template>
  </v-data-table>

	<div class="text-xs-center pt-2">
      <v-pagination v-model="pagination.page" :length="pages"></v-pagination>
    </div>

      </v-layout>
    </v-slide-y-transition>
  </v-container>

</template>

<script>
import axios from 'axios';

  export default {
    data () {
      return {
pagination: {
},
        info : null,
        headers: [
          {
            text: 'Beer',
            align: 'left',
            sortable: false,
            value: 'name'
          },
        ]
      }
    },
    computed: {
      pages () {
        if (this.pagination.rowsPerPage == null ||
          this.pagination.totalItems == null
        ) return 0

        return Math.ceil(info.length / this.pagination.rowsPerPage)
      }
},
 mounted () {
      axios
        .get('https://api.punkapi.com/v2/beers?malt=extra_pale')
        .then(response => (this.info = response.data))
    }
   }


</script>


