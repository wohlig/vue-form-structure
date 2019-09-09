<template>
  <div class="container">
    <div class="column">
      <div class="card inception">
        <h3 class="tab-heading inception">
          <div class="text">Personal Details</div>
        </h3>
        <div class="text-left main-form-section mx-5">
          <b-form
            name="form"
            @submit="onSubmit()"
            @reset="onReset()"
            v-if="show"
          >
            <!-- first name -->
            <b-form-group label="First Name:" label-for="firstName">
              <b-form-input
                id="firstName"
                v-model="form.firstName"
                type="text"
                required
                placeholder="Enter First Name"
              ></b-form-input>
              <div
                v-if="$v.form.firstName.$error && !$v.form.firstName.required"
                class="error-txt"
              >
                first name is required
              </div>
            </b-form-group>

            <!-- middle name -->
            <b-form-group label="Middle Name:" label-for="middleName">
              <b-form-input
                id="middleName"
                type="text"
                v-model="form.middleName"
                required
                placeholder="Enter Last Name"
              ></b-form-input>
              <div
                v-if="$v.form.middleName.$error && !$v.form.middleName.required"
                class="error-txt"
              >
                first name is required
              </div>
            </b-form-group>

            <!-- last name -->
            <b-form-group label="Last Name:" label-for="lastName">
              <b-form-input
                id="lastName"
                type="text"
                v-model="form.lastName"
                required
                placeholder="Enter Last Name"
              ></b-form-input>
              <div
                v-if="$v.form.lastName.$error && !$v.form.lastName.required"
                class="error-txt"
              >
                first name is required
              </div>
            </b-form-group>
            <!-- gender -->
            <b-form-group label="Select Gender">
              <div class="d-flex">
                <div>
                  <b-form-radio
                    v-model="form.selectedGender"
                    name="some-radios"
                    value="A"
                    >Male</b-form-radio
                  >
                </div>
                <div class="ml-5">
                  <b-form-radio
                    v-model="form.selectedGender"
                    name="some-radios"
                    value="B"
                    >Female</b-form-radio
                  >
                </div>
              </div>
              <div
                v-if="
                  $v.form.selectedGender.$error &&
                    !$v.form.selectedGender.required
                "
                class="error-txt"
              >
                gender is required
              </div>
            </b-form-group>
            <!-- email -->
            <b-form-group label="Email" label-for="email">
              <b-form-input
                id="email"
                type="email"
                v-model="form.email"
                required
                placeholder="Enter Email"
              ></b-form-input>
              <div
                v-if="$v.form.email.$error && !$v.form.email.required"
                class="error-txt"
              >
                gmail is required
              </div>
            </b-form-group>
            <!-- password -->
            <b-form-group label="Password" label-for="password">
              <b-form-input
                id="password"
                type="password"
                v-model="form.password"
                required
                placeholder="Enter Password"
              ></b-form-input>
              <div
                v-if="$v.form.password.$error && !$v.form.password.required"
                class="error-txt"
              >
                password is required
              </div>
            </b-form-group>
            <!-- date -->
            <b-form-group label="age" label-for="age">
              <div class="d-flex w-50">
                <div class="w-50">
                  <b-form-group
                    class
                    id="calendar"
                    name="calendar"
                    label="Date Of Birth"
                    required
                  >
                    <date-picker
                      v-model="form.dob"
                      v-on:change="selectDate(form.dob)"
                      type="number"
                      :lang="'es'"
                      :first-day-of-week="1"
                      :format="'YYYY-MM-DD'"
                      class
                      :placeholder="'Select Date'"
                    ></date-picker>
                  </b-form-group>
                </div>
                <div class="ml-4 w-50">
                  <b-form-group label="age" label-for="age">
                    <b-form-input
                      id="age"
                      type="text"
                      v-model="form.age"
                      required
                      placeholder="age"
                    ></b-form-input>
                  </b-form-group>
                </div>
              </div>
              <div
                v-if="$v.form.dob.$error && !$v.form.dob.required"
                class="error-txt"
              >
                first select date
              </div>
            </b-form-group>
            <!-- mobile no -->
            <b-form-group label="Mobile No" label-for="mobileNO">
              <b-form-input
                id="mobileNO"
                type="number"
                v-model="form.mobileNO"
                required
                placeholder="Enter Mobile no  "
              ></b-form-input>
              <div
                v-if="$v.form.mobileNO.$error && !$v.form.mobileNO.required"
                class="error-txt"
              >
                mobile no is required
              </div>
            </b-form-group>

            <!-- subnit and reset button -->
            <div>
              <b-button
                type="submit"
                v-on:click="onSubmit(form)"
                to="#"
                variant="primary"
                >Submit</b-button
              >
              <b-button class="ml-4" type="reset" variant="danger"
                >Reset</b-button
              >
            </div>
          </b-form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { required } from "vuelidate/lib/validators";
import DatePicker from "vue2-datepicker";

import moment from "moment";
export default {
  components: { DatePicker },
  data() {
    return {
      show: true,
      errors: [],
      bootstrapBtnPromise: "",
      submitStatus: "true",

      form: {
        firstName: "",
        middleName: "",
        lastName: "",
        selectedGender: "",
        email: "",
        password: "",
        dob: "",
        age: "",
        mobileNO: "",
        checked: []
      },

      // date picker script
      selectedGender: "",
      value: "",
      time1: "",
      time2: "",
      time3: "",
      // custom lang
      lang: {
        days: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
        months: [
          "Jan",
          "Feb",
          "Mar",
          "Apr",
          "May",
          "Jun",
          "Jul",
          "Aug",
          "Sep",
          "Oct",
          "Nov",
          "Dec"
        ],
        pickers: [
          "next 7 days",
          // "next 30 days",
          "previous 7 days",
          "previous 30 days"
        ]
      },
      // custom range shortcuts
      shortcuts: [
        {
          text: "Today",
          onClick: () => {
            this.time3 = [new Date(), new Date()];
          }
        }
      ],

      foods: [
        { text: "Select One", value: null },
        "Carrots",
        "Beans",
        "Tomatoes",
        "Corn"
      ]
    };
  },

  validations: {
    form: {
      firstName: {
        required
      },
      lastName: {
        required
      },
      middleName: {
        required
      },
      selectedGender: {
        required
      },
      email: {
        required
      },
      password: {
        required
      },
      dob: {
        required
      },
      mobileNO: {
        required
      }
    }
  },

  methods: {
    onSubmit() {
      this.$v.form.$touch();
      if (this.$v.form.$error) {
        return;
      }
    },

    onReset(evt) {
      evt.preventDefault();
      // Reset our form values
      this.form.firstName = "";
      this.form.middleName = "";
      this.form.lastName = "";
      this.form.selectedGender = "";
      this.form.email = "";
      this.form.password = "";
      this.form.dob = "";
      this.form.age = "";
      this.form.mobileNO = "";
      this.form.checked = [];
      // Trick to reset/clear native browser form validation state
      this.show = true;
      this.$nextTick(() => {
        this.show = true;
      });
    },
    selectDate: function(value) {
      this.form.age =
        moment(new Date()).format("YYYY") - moment(value).format("YYYY");
    }
  }
};
</script>
<style lang="scss" scoped>
@import "src/assets/scss/main.scss";
.error-txt {
  color: red;
}

.main-form-section {
  color: $black !important;
}

.card {
  font-size: 1.1rem;
  font-weight: 400;
  margin: 7rem 0;
  padding: 0 0 1rem 0;
  width: 100%;
  box-shadow: 0.3rem 1.3rem 2rem 2px rgba(56, 65, 56, 0.41);
  background-color: $light-white;
  p {
    margin: 0 1rem 1rem 1rem;
    color: #333;
    font-size: 1.2rem;
    font-weight: 300;
    &:last-child {
      margin-bottom: 0;
    }
  }
}

.tab-heading {
  font-family: "Open Sans";
  font-weight: 600;
  border-top: 0.3rem solid #03a9f4;
  margin: 0 0 1rem 0;
  color: $fg-color;
  background-color: transparent;
  display: flex;
  justify-content: flex-start;

  position: relative;
  &:before,
  &:after {
    content: "";
    display: block;
    width: 1rem;
    height: 1rem;
    background-color: transparent;
    background-image: $inverted-corner;
    background-size: contain;
    background-repeat: no-repeat;
    margin-top: -1px;
  }
  &:before {
    margin: 0 0 0 1rem;
  }
  &:after {
    transform: rotateZ(270deg);
  }
  .text {
    display: block;
    background-color: $heading-bg-color;
    padding: 0.2rem 1rem 0.5rem;
    border-color: $heading-bg-color;
    border-bottom-right-radius: 1rem;
    border-bottom-left-radius: 1rem;
    position: relative;
    box-shadow: 0.1rem 0.4rem 0.5rem -3px rgba(0, 0, 0, 0.56);
    margin-top: -1px;
    &:before,
    &:after {
      content: "";
      display: block;
      position: absolute;
      z-index: -1;
    }
    &:before {
      bottom: 0.4rem;
      right: 0.9rem;
      width: 75%;
      height: 1.6rem;
      box-shadow: 0.8rem 0.4rem 1rem -0.9px rgba(0, 0, 0, 0.76);
      transform: rotate(6deg);
      border-bottom-right-radius: 1rem;
    }
    &:after {
      top: -0.7rem;
      right: 0.65rem;
      transform: rotate(20deg);
      content: "(";
      color: transparent;
      font-size: 1.7rem;
      font-weight: 900;
      text-shadow: 1rem 0 0.4rem black;
    }
  }
}
</style>
