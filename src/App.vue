<template>
  <div id="app">
    <div class="title">
      <img
        src="https://cdn.bookingkit.net/wp-content/themes/bookingkit/images/bookingkit_logo.png"
        alt="">
    </div>
    <div class="grid-container">
      <div class="box1">
        <BookingForm :addBooking="addBooking" />
      </div>
      <div class="box2">
        <BookingsList
          :bookingsList="bookingsList"
          :deleteBooking="deleteBooking" />
      </div>
      <div class="box3">
        <BookingsStatics
          :chartData="chartData"
          :months="months"/>
      </div>
    </div>
  </div>
</template>

<script>
import BookingForm from './components/BookingForm.vue';
import BookingsList from './components/BookingsList';
import BookingsStatics from './components/BookingsStatics';

export default {
  name: 'App',
  components: {
    BookingForm,
    BookingsList,
    BookingsStatics
  },
  data() {
    return {
      bookingsList: [
        { id: 1,firstname: 'Lee', lastname: 'Sin', date: '2021-03-16'},
        { id: 2,firstname: 'Tahm', lastname: 'Kench', date: '2021-03-17'},
        { id: 3,firstname: 'Miss', lastname: 'Fortune', date: '2021-03-11'},
      ],
      months: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
      chartData: [],
    }
  },

  created() {
    this.proccessData();
  },

  methods: {
    deleteBooking(booking) {
      const filteredBookings = this.bookingsList.filter( b => b !== booking);
      this.bookingsList = filteredBookings;
      this.proccessData();
    },
    addBooking(firstname, lastname, date) {
      this.bookingsList.push({
        id: this.bookingsList.length + 1,
        firstname,
        lastname,
        date,
      });
      this.proccessData();
    },
    proccessData() {
      this.chartData = [];
      this.months.forEach( async (_month, index) => {
      let counter = 0;
        this.bookingsList.forEach((booking, bookingIndex) => {
          const bookingMonth = booking.date.split("-")[1];
          const month = index >= 9 ? index + 1 : `0${index + 1}`;
          counter = bookingMonth == month ? counter + 1 : counter;
          this.bookingsList.length === bookingIndex + 1 && this.chartData.push(counter.toString());
        });
      });
    }
  }
}
</script>

<style>
html, body {
    max-width: 100%;
    overflow-x: hidden;
}

.title {
  position: relative;
  left: 1%;
  height: 51px;
}
.grid-container {
  background-color: #eee;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 0px 0px;
  grid-template-areas:
    "box1 box3"
    "box2 box3";
}

.box1 { grid-area: box1; }

.box2 { grid-area: box2; }

.box3 { grid-area: box3; }
@media only screen and (max-width: 1024px) {
  .grid-container {
    display: inline;
  }
}
</style>
