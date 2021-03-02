<template>
  <div class="form-container">
    <div>
      <b-form>
        <b-form-input
          v-model="firstname"
          class="input"
          placeholder="Firstname"
          required
        />
        <br>
        <b-form-input
          v-model="lastname"
          class="input"
          placeholder="Lastname"
          required
        />
        <br>
        <b-form-datepicker
          :min="min"
          :max="max"
          id="example-datepicker"
          v-model="date"
          class="mb-2"
          placeholder="Select a date"
          required
        />
        <br>
        <b-button
          class="submit-btn"
          :disabled="!isFormFilled"
          @click="addBooking(firstname, lastname, date)"
        >
          Add booking
        </b-button>
      </b-form>
    </div>
</div>
</template>

<script>
export default {
  name: 'BookingForm',
  props: {
    addBooking: Function,
  },
  data() {
    return {
      firstname: null,
      lastname: null,
      date: null,
      min: new Date(2021, 0, 1),
      max: new Date(2021, 11, 31)
    }
  },
  computed: {
    isFormFilled() {
      return this.firstname && this.lastname && this.date;
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.form-container {
 position: relative;
 left: 5%;
 top:10%;
}
.submit-btn {
  width: 90%;
  background-color: white  !important;
  color: black !important;
  border-radius: 15px !important;
}
.input, .mb-2{
    width: 90%;
}
</style>
