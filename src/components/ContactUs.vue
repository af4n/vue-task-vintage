<template>
	<div class="contact-us">
		<div class="container">
			<div class="form">
				<h2>Contact Us</h2>
				<form action="http://httpbin.org/post" method="POST" @submit.prevent="submitHandler">
					<div class="form-group">
						<label class="form__label" :style="focusedName ? 'color: #ffffff' : ''">Name</label>
						<input
							type="text"
							class="form__input"
							@focus="focusedName = true"
							@blur="focusedName = false"
							v-model.trim="$v.name.$model">
					</div>
					<div class="error" v-if="!$v.name.required && $v.name.$anyError">Field is required.</div>
					<div class="error" v-if="!$v.name.alpha">The name must be only letters.</div>
					<div class="error" v-if="!$v.name.maxLength">Field must have no more than {{
						$v.name.$params.maxLength.max
						}} characters.
					</div>
					<div class="form-group">
						<label class="form__label" :style="focusedPhone ? 'color: #ffffff' : ''">Phone</label>
						<input
							type="tel"
							class="form__input"
							id="phone"
							v-imask="phoneNumberMask"
							@keypress="isNumber"
							@accept="onAccept"
							@complete="onComplete"
							@focus="focusedPhone = true"
							@blur="focusedPhone = false"
							maxlength="19"
							v-model.trim="$v.phone.$model">
					</div>
					<div class="error" v-if="!$v.phone.required && $v.phone.$anyError">Field is required.</div>
					<div class="error" v-if="!$v.phone.minLength">Please enter a valid phone number.</div>

					<div class="form-group">
						<label class="form__label" :style="focusedEmail ? 'color: #ffffff' : ''">Email</label>
						<input
							type="email"
							class="form__input"
							@focus="focusedEmail = true"
							@blur="focusedEmail = false"
							v-model.trim="$v.email.$model">
					</div>
					<div class="error" v-if="!$v.email.required && $v.email.$anyError">Field is required.</div>
					<div class="error" v-if="!$v.email.email">Please enter a valid email address.</div>
					<div class="form-group form__checkbox">
						<input
							type="checkbox"
							class="form__checkbox-input"
							id="checkbox-input"
							v-model.trim="$v.checkbox.$model">
						<label class="form__checkbox-label" for="checkbox-input">I agree the processing of personal data</label>
					</div>
					<button type="submit" :disabled="formValid">Get in touch</button>
				</form>
			</div>
			<div class="about-you">
				<p>Please tell us more about your request and give us info about your <br> company and country</p>
			</div>
		</div>
	</div>
</template>

<script>
  import {required, alpha, minLength, maxLength, email, sameAs} from 'vuelidate/lib/validators';
  import {IMaskDirective} from 'vue-imask';

  export default {
    name: 'ContactUs',
    data() {
      return {
        name: '',
        phone: '',
        email: '',
        checkbox: false,
        focusedName: false,
        focusedPhone: false,
        focusedEmail: false,
        phoneNumberMask: {
          mask: '+{38 (0}00) 000-00-00'
        }
      }
    },
    directives: {
      imask: IMaskDirective
    },
    validations: {
      name: {
        required,
        alpha,
        maxLength: maxLength(30)
      },
      phone: {
        required,
        minLength: minLength(19)
      },
      email: {
        required,
        email
      },
      checkbox: {
        required,
        sameAs: sameAs(() => true)
      }
    },
    computed: {
      formValid() {
        return this.$v.$invalid
      }
    },
    methods: {
      onAccept(e) {
        const maskRef = e.detail
        this.phone = maskRef.value
      },
      onComplete(e) {
        const maskRef = e.detail
        this.userPhone = maskRef.unmaskedValue
      },
      isNumber(e) {
        let regex = /[0-9]/

        if (!regex.test(e.key)) {
          e.returnValue = false;
          if (e.preventDefault) e.preventDefault();
        }
      },
      submitHandler() {
        const formPayload = {
          name: this.name,
          phone: this.phone,
          email: this.email,
          checkbox: this.checkbox,
        }
        this.name = ''
        this.phone = ''
        this.email = ''
        this.checkbox = false
        alert('Request sent successfully')
        console.log('formPayload:', formPayload)
      }
    }

  }
</script>

<style scoped lang="scss">

	.contact-us {
		background: url("../assets/images/bg-contact-us.png");
		padding-top: 100px;
		padding-bottom: 100px;

		.container {
			display: flex;

			.form {
				width: 50%;
				color: #ffffff;

				h2 {
					margin-bottom: 20px;
				}

				.form-group {
					margin-bottom: 10px;

					.form__label {
						font-size: 18px;
						color: #000000;
						border-bottom: 1px solid #040707;
						padding-bottom: 13.5px;
						height: 50px;
						transition: all 0.5s ease-out;

					}

					.form__input {
						width: 400px;
						background-color: transparent;
						border: none;
						font-family: SuisseIntl-Light, Helvetica, Arial, sans-serif;
						font-size: 18px;
						border-bottom: 1px solid #040707;
						padding-left: 50px;
						height: 50px;
						transition: all 0.5s ease-out;


						&:focus {
							outline: none;
							color: #ffffff;
						}
					}
				}

				.form__checkbox {

					&-input {
						position: relative;
						margin-right: 20px;
						font-size: 15.3333px;
						transition: all 0.5s ease-out;

						&:before {
							content: '';
							width: 15px;
							height: 15px;
							position: absolute;
							left: 0;
							top: 0;
							background-image: url('../assets/images/unchecked.png');
							background-repeat: no-repeat;
							transition: all 0.5s ease-out;
						}

						&:checked {
							background-image: none;
						}

						&:checked:before {
							content: '';
							width: 15px;
							height: 15px;
							position: absolute;
							left: 0;
							top: 0;
							background-image: url('../assets/images/checked.png');
							background-repeat: no-repeat;
							transition: all 0.5s ease-out;

						}
					}


					&-label {
						font-size: 18px;
						line-height: 34px;
					}
				}

				.error {
					color: #C14242;
					font-size: 14px;
					transition: all 0.5s ease-out;
				}

				button {
					font-family: SuisseIntl-SemiBold;
					letter-spacing: 1px;
					color: #ffffff;
					background: #262626;
					padding: 35px 90px;
					margin-top: 40px;
					border: none;
					text-transform: uppercase;
					transition: all 0.5s ease-out;
					cursor: pointer;

					&:disabled {
						opacity: 0.7;
						cursor: not-allowed;
					}
				}
			}

			.about-you {
				width: 50%;
				margin-top: 75px;

				p {
					font-size: 18px;
					line-height: 34px;
				}
			}
		}
	}

	@media (max-width: 1050px) {
		.contact-us .container .form .form-group .form__input {
			max-width: 300px;
		}
	}

	@media (min-width: 769px) and (max-width: 991px) {
		.contact-us .container .form .form-group .form__input {
			width: 200px;
		}
	}

	@media (max-width: 768px) {
		.contact-us .container {
			flex-direction: column;
			padding: 0 30px;

			.form {
				width: 100%;

				.form-group .form__input {
					width: 400px;
				}
			}

			.about-you {
				width: 100%;
			}
		}
	}

	@media (max-width: 540px) {
		.contact-us .container .form .form-group .form__input {
			width: 200px;
		}

		.contact-us .container .form button {
			padding: 25px 45px;
		}
	}

	@media (max-width: 480px) {
		.contact-us .container .form .form-group .form__label {
			font-size: 15px;
			padding-bottom: 15.5px;
		}

		.contact-us .container .form .form-group .form__input {
			width: 180px;
			font-size: 15px;
			padding-left: 20px;
		}

		.contact-us .container .form .form__checkbox-label {
			font-size: 15px;
			line-height: 24px;
		}
	}
</style>
