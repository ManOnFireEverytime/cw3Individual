<template>
            <section class="py-5">
          <div class="container px-4 px-lg-5 mt-5">
            <div
              class="row gx-4 gx-lg-5 row-cols-2 row-cols-md-3 row-cols-xl-4 justify-content-center"
            >
              <div v-for="item in cart"  :key="item.id" class="col mb-5">
                <div class="card h-100">
                  <img
                    v-bind:src="urls + item.lesson.image"
                    class="card-img-top"
                  />

                  <div class="card-body p-4">
                    <div class="text-center">
                      <h5 class="fw-bolder">Subject: {{ item.lesson.topic }}</h5>
                      <p><font-awesome-icon v-bind:icon="item.lesson.icon" /></p>

                      <p>Location: {{ item.lesson.location }}</p>
                      <p>Spaces: {{ item.space }}</p>
                      Price: £{{ item.lesson.price }}
                    </div>
                  </div>
                  <div class="card-footer p-4 pt-0 border-top-0 bg-transparent">
                    <div class="text-center">
                      <a
                        class="btn btn-outline-dark mt-auto"
                        v-on:click="removeFromCart(item.lessonId)"
                        >Remove From Cart</a
                      >
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>        
          <section>
          <div class="container">
            <div class="py-5 text-center">
              <h2>Checkout</h2>
            </div>

            <div class="row">
              <div class="col-md-12 order-md-1">
                <form class="needs-validation">
                  <div class="row">
                    <div class="col-md-6 mb-3">
                      <input
                        name="name"
                        type="text"
                        v-model="name"
                        class="form-control"
                        placeholder="Name"
                      />
                    </div>
                    <div class="col-md-6 mb-3">
                      <input
                        name="phone"
                        type="text"
                        v-model="phone"
                        class="form-control"
                        placeholder="Phone"
                      />
                    </div>
                  </div>
                  <button
                    class="col-md-12 mb-5 btn btn-primary btn-lg btn-block"
                    v-if="enableCheckoutButton"
                    id="btn"
                    type="submit"
                    v-on:click="submitForm"
                    
                  >
                    Checkout
                  </button>
                  <button
                    class="col-md-12 mb-5 btn btn-primary btn-lg btn-block"
                    v-else
                    id="btn"
                    type="submit"
                    disabled
                    
                  >
                    Checkout
                  </button>
                </form>
              </div>
            </div>
          </div>
        </section>
        </section>

</template>

<script>
export default {
  name: "app",
  data(){
    return{
        name: "",
        phone: "",
    }
  },
  props: ["filteredLessons", "urls", "cart"],
  methods: {
        // validate name
        validateNameInput() {
            let result = /^[A-Za-z_ ]{2,90}$/.test(this.name);
            return result;
        },
        // validate phone
        validatePhoneInput() {
            let result = /^\d{9,11}$/.test(this.phone);
            return result;
        },
    // removes a lesson from cart
    removeFromCart(lessonId) {
        this.$emit("remove-item-from-cart", lessonId)
    },
    submitForm() {
      alert("Your order has been Submitted");
    },
  },
  computed: {
    enableCheckoutButton: function () {
            var nameIsValid = this.validateNameInput();
            var phoneIsValid = this.validatePhoneInput();

            if (nameIsValid && phoneIsValid) {
                return true;
            }
            return false
        }
  }

};

</script>