<template>
	<button :class="computedClass" :id="id" :type="type" :disabled="!loaded || disabled" :ref="reference" @click.prevent="click">
		<div :id="recaptchaId" data-size="invisible"/>
		<slot></slot>
	</button>
</template>

<script type="text/javascript">
	export default {
		props: {
			sitekey: {
				type: String,
				required: true
			},

			badge: {
				type: String,
				required: false,
				default: 'bottomright',
			},

			theme: {
				type: String,
				required: false,
				default: 'dark',
			},

			validate: {
				type: Function,
				required: false,
			},

			callback: {
				type: Function,
				required: true
			},

			disabled: {
				type: Boolean,
				required: false,
				default: false,
			},

			id: {
				type: String,
				required: false,
			},
			
			reference: {
				type: String,
				required: false
			},
			
			type: {
				type: String,
				required: false,
				default: 'submit',
			}
		},

		data: function() {
			return {
				widgetId: false,
				loaded: false
			};
		},

		methods: {
			render: function() {
				this.widgetId = grecaptcha.render(this.recaptchaId, {
					sitekey: this.sitekey,
					size: 'invisible',
					badge: this.badge,
					theme: this.theme,
					callback: token => {
						this.callback(token);
						grecaptcha.reset(this.widgetId);
					}
				});
				this.loaded = true;
			},

			renderWait: function() {
				const self = this;
				setTimeout(function() {
					if (typeof grecaptcha !== 'undefined' && grecaptcha.render) self.render();
					else self.renderWait();
				}, 200);
			},

			click: function() {
				if (!this.validate || this.validate && this.validate() !== false)
					grecaptcha.execute();
			}
		},

		computed: {
			computedClass: function() {
				var classArray = this.class ? this.class.split(' ') : [];

				if (this.value) {
					classArray.push('invisible-recaptcha');
				}

				return classArray;
			},
			recaptchaId: function() {
				return 'vue-invisible-recaptcha-' + this._uid;
			}
		},

		mounted: function() {
			if (typeof grecaptcha === 'undefined') {
				var script = document.createElement('script');
				script.src = 'https://www.google.com/recaptcha/api.js?render=explicit';
				script.onload = this.renderWait;

				document.head.appendChild(script);
			} else this.render();
		}
	};
</script>
