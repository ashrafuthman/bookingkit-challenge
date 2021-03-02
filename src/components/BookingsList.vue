<template>
  <div>
    <b-table
      class="table"
      striped
      hover
      :items="bookingsList"
      :fields="fields"
      :sticky-header="true"
    >
      <template #cell(actions)="bookingData">
        <b-button
          class="delete-btn"
          @click="deleteBooking(bookingData.item)"
          variant="warning"
        >
          X
        </b-button>
      </template>
    </b-table>
  </div>
</template>

<script>
  export default {
    name: 'BookingsList',
    props: {
      bookingsList: Array,
      deleteBooking: Function,
    },
    data() {
      return {
        fields: [
          {
            key: 'lastname',
            sortable: true,
          },
          {
            key: 'firstname',
            sortable: true,
          },
          {
            key: 'date',
            label: 'date',
            sortable: true,
          },
          {
            key: 'actions',
            label: 'actions',
            sortable: false,
          }
        ],
      }
    },
  }
</script>

<style scoped>
.table {
  width: 90%;
  position: relative;
  top: 5%;
  left: 5%;
  margin-bottom: 1rem;
  color: #212529;
}
.delete-btn {
  color: white;
  font-weight: bolder;
}
</style>
