<template>
    <form @submit.prevent="onSubmit" :class="'status-'+status">
        <div class="content">
            <div><input type="email" placeholder="Your email" v-model="email" name="email" required class="block"/></div>
            <label class="label">
                <input type="checkbox" class="big" required  name="agreement" />
                <span class="text-small">{{$ts('I agree to receive email communications from Robonomics')}}</span>
            </label>
            <div>
                <vue-recaptcha
                    ref="invisibleRecaptcha"
                    @verify="onVerify"
                    size="invisible"
                    :sitekey="recaptchaSitekey" />

                <Button button="primary block green large">
                        <span class="text">{{$ts('Submit')}}</span>
                    </Button>

                <!-- <vue-recaptcha :sitekey="recaptchaSitekey">
                    <Button button="primary block green large">
                        <span class="text">{{$ts('Submit')}}</span>
                    </Button>
                </vue-recaptcha> -->
            </div>
        </div>

        <div class="load">
        <div class="load-bird">
            <g-image src="/assets/kusama-karate-body.png" class="bird-body"/>
            <g-image src="/assets/kusama-karate-tale.png" class="bird-tale"/>
            <g-image src="/assets/kusama-karate-wing-1.png" class="bird-wing-1"/>
            <g-image src="/assets/kusama-karate-wing-2.png" class="bird-wing-2"/>
            <g-image src="/assets/kusama-karate-ribbons.png" class="bird-ribbons"/>
            <g-image src="/assets/kusama-karate-hair.png" class="bird-hair"/>
            <g-image src="/assets/kusama-karate-leg.png" class="bird-leg"/>
        </div>
        <p><b>You are in the list now. We'll send you email with updates.</b></p>
        </div>

        <div class="wait"><g-image src="~/assets/images/robonomics.png" area-hidden="true"/></div>
        <div class="error">Something went wrong. Please, check your connection or try later.</div>

    </form>
</template>

<script>
// import { VueRecaptcha } from 'vue-recaptcha';

export default {
    components: {
    //   VueRecaptcha,
      VueRecaptcha: () => import("vue-recaptcha"),
      Button: () => import("~/components/Button.vue")
    },

    metaInfo: {
      script: [
        {
          src: 'https://www.google.com/recaptcha/api.js?onload=vueRecaptchaApiLoaded&render=explicit',
          async: true,
          defer: true,
          body: true
        }
      ]
    },

    data () {
      return {
        email: null,
        status: 'none',
        //  recaptchaSitekey: "6LeWbWQUAAAAAPkpf_6AokhGBcvnOexOpbARwk6Z",
        recaptchaSitekey: "6LeIxAcTAAAAAJcZVRqyHh71UMIEGNQ_MXjiZKhI" //test localhost
      }
    },

    methods: {

      //add email to whitelist
      onSubmit: function() {
        console.log('onSubmit')
        console.log(this.$refs.invisibleRecaptcha)
        this.$refs.invisibleRecaptcha.execute()
      },

      onVerify: function (response) {
        console.log('onVerify')
        if(response) {
          this.status = 'wait'
            let request = ''
            if(this.email){
              request = 'email=' + encodeURIComponent(this.email)
            }
            fetch('https://script.google.com/macros/s/AKfycbxpBhEciQcoPzDy0VQRhVH_I9NBlwUP3lvjD0GfnRYbv2xlT_ZKx3StV6oqPEFHTJESVg/exec', {
              method: 'POST',
              headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
              body: request
            })
            .then(() => this.status = 'load')
            .catch(error => this.status = 'error')
          }
      },
    }

}
</script>

<style scoped>
    form, .content {
        position: relative;
    }

    .content {
        z-index: 0;
    }

  .load, .wait, .error {
    visibility: hidden;
    height: 0;
    opacity: 0;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1;
  }

  .load { text-align: center; color: var(--color-red) }

  .load-bird {
    position: relative;
    /* top: -24px;
    left: calc(50% - 74px); */
    width: 148px;
    height: 180px;
    margin: 0 auto;
    transform: scale(0.7);
  }
  
  .load-bird img { position: absolute; }
  .load-bird img:not(.bird-body) {
    animation-delay: 0.6s;
    animation-duration: 0.8s;
    animation-timing-function: cubic-bezier(0.075, 0.82, 0.165, 1);
    animation-fill-mode: forwards;
  }
  .bird-body {
    width: 148px;
    top: 0;
    left: 0;
    z-index: 1;
  }
  .bird-tale {
    width: 58px;
    top: 100px;
    left: -35px;
    z-index: 0;
    transform-origin: 0 100%;
  }
  .bird-wing-1 {
    width: 47px;
    top: 42px;
    left: 23px;
    z-index: 2;
    transform-origin: 0 0;
  }
  .bird-wing-2 {
    width: 67px;
    top: 42px;
    left: 120px;
    z-index: 0;
    transform-origin: 0 0;
  }
  .bird-ribbons {
    width: 63px;
    top: 37px;
    left: -8px;
    z-index: 0;
    transform-origin: 100% 50%;
  }
  .bird-hair {
    width: 14px;
    top: -10px;
    left: 72px;
    z-index: 0;
    transform-origin: 100% 50%;
  }
  .bird-leg {
    width: 37px;
    top: 127px;
    left: 63px;
    z-index: 3;
    transform-origin: 100% 0;
  }


  .status-load .load {
    animation: FadeIn 0.3s var(--animation-bump) forwards;
  }

  .status-load .load .bird-tale { animation-name: birdTale; }
  .status-load .load .bird-wing-1 { animation-name: birdWing1; }
  .status-load .load .bird-wing-2 { animation-name: birdWing2; }
  .status-load .load .bird-ribbons { animation-name: birdRibbons; }
  .status-load .load .bird-hair { animation-name: birdHair; }
  .status-load .load .bird-leg { animation-name: birdLeg; }

  .status-load .content { pointer-events: none; opacity: 0.1; }

  .wait {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-content: center;
      align-items: center;
    }

   .wait img {
        width: 90px;
        animation: pulse 1.5s infinite;
      }

  .status-wait .wait {
    animation: FadeIn 0.3s var(--animation-bump) forwards;
  }

  .status-wait > *:not(.wait), .status-wait button { pointer-events: none; opacity: 0.5; }

  .status-error .error {
        animation: FadeIn 0.3s var(--animation-bump) forwards;
        color: var(--color-red);
        height: auto;
      }

  @keyframes birdTale {
    to{
      transform: rotate(25deg) translateX(-20px) translateY(-20px);
    }
  }
  @keyframes birdWing1 {
    to{
      transform: rotate(-50deg) translateX(-25px) translateY(-10px);
    }
  }
  @keyframes birdWing2 {
    to{
      transform: rotate(-50deg) translateX(-25px) translateY(30px);
    }
  }
  @keyframes birdRibbons {
    to{
      transform: rotate(30deg) translateX(-20px);
    }
  }
  @keyframes birdHair {
    to{
      transform: rotate(-30deg);
    }
  }
  @keyframes birdLeg {
    to{
      transform: rotate(-110deg) translateX(10px) translateY(20px);
    }
  }

  /* end of email form */

</style>