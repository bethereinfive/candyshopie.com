<template>
    <div>
    <!-- <section id="call">
      <img :src="$asseturl+'frontend/img/phone.png'" alt="phone" />
    </section> -->

        <slot></slot>

<section style="padding: 40px;"></section>
        <section id="menus">
            <div class="container-fluid">
                <div class="row">
                    <div class="col-3 p-0" style="width: 20% !important;">
                        <div class="menu">
                            <router-link :to="{name:'Authuser'}" class="navIcon">
                                <i class="fa-solid fa-table-columns"></i>
                                <p>Home</p>
                            </router-link>
                        </div>
                    </div>
                    <div class="col-3 p-0" style="width: 20% !important;">
                        <div class="menu">
                            <router-link :to="{name:'UserTeam'}" class="navIcon">
                                <i class="fa-brands fa-steam-symbol"></i>
                                <p>Team</p>
                            </router-link>
                        </div>
                    </div>
                    <div class="col-3 p-0" style="width: 20% !important;">
                        <div class="menu">
                            <router-link :to="{name:'Usertask'}" class="navIcon">
                                <i class="fa-solid fa-list-check"></i>
                                <p>Tasks</p>
                            </router-link>
                        </div>
                    </div>
                    <div class="col-3 p-0" style="width: 20% !important;">
                        <div class="menu">
                            <router-link :to="{name:'support'}"  class="navIcon">

                                <i class="fa-solid fa-handshake-angle"></i>
                                    <p>Help</p>
                                </router-link>
                        </div>
                    </div>
                    <div class="col-3 p-0" style="width: 20% !important;">
                        <div class="menu">
                            <router-link :to="{name:'Useraccount'}" class="navIcon">
                                <i class="fa-solid fa-circle-info"></i>
                                <p>Account</p>
                            </router-link>
                        </div>
                    </div>


                </div>
            </div>
        </section>

    </div>
</template>
<script>
  export default {
    created() {
                this.createlink('frontend/css/bootstrap.min.css');
        this.createlink('frontend/css/style.css?ver=1.3');
        this.createlink('frontend/css/font-awesome.min.css');

        this.createscript('frontend/js/bootstrap.bundle.min.js');
        this.createscript('frontend/js/bootstrap.min.js');
    },
    data(){
        return {

        }},
    watch: {
        '$route': {
            handler(newValue, oldValue) {
                window.scrollTo(0,0);
            },
            deep: true
        }
    },
    mounted() {


    },
    methods: {
        createlink(url=''){
            let recaptchaScript = document.createElement('link')
            recaptchaScript.setAttribute('href', this.$asseturl+url)
            recaptchaScript.setAttribute('rel', 'stylesheet')
            document.head.appendChild(recaptchaScript)
        },
        createscript(url=''){
            let recaptchaScript = document.createElement('script')
            recaptchaScript.setAttribute('src', this.$asseturl+url)
            document.body.appendChild(recaptchaScript)
        }
    }
  }
</script>
<style>
.col-6.amount_item span {
  border: 2px solid #e8ba31;
  display: block;
  text-align: center;
  margin: 6px 0px;
  padding: 4px 3px;
  cursor: pointer;
}


input.money-btn {
    border: 1px solid red;
    color: red !important;
}
button.money-btn {
    padding: 1px 20px;
    margin: 11px 0px;
    font-size: 23px;
    background: #E02A65;
    color: white;
    width: 100%;
    border-radius: 21px;
}
section.intro.profileBg.mb-5,.layout-content {
    width: 90%;
    margin: 42px auto;
}
section.intro.profileBg.mb-5 {
    padding: 35px 0px;
}
.step{
    color:white;
}

a.navIcon i {
    font-size: 25px;
    color: #2e6800;
    margin-bottom: 10px;
}

</style>
