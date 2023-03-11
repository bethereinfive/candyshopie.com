<template>
  <div>


    <section id="slider">
        <img width="100%" :src="slideimage" alt="">
    </section>

    <section id="marquee">
      <div class="container-fluid">
        <div class="marquee-area">
          <div class="left-img">
            <img :src="$asseturl+'frontend/img/notice_icon.png'" alt="icon" />
          </div>
          <marquee>{{ settings.notice }}</marquee
          >
          <div class="button right">Notice</div>
        </div>
      </div>
    </section>

    <section id="aui">
      <div class="container-fluid">
        <div class="row">
          <div class="col-3 p-0">
            <router-link :to="{name:'Recharge'}" class="linkColor">
                <i class="fa-sharp fa-solid fa-file-invoice-dollar"></i>
              <span>Recharge</span>
            </router-link>
          </div>
          <div class="col-3 p-0">
            <router-link :to="{name:'Withdraw'}" class="linkColor">
                <i class="fa-solid fa-money-bill-transfer"></i>
              <span>Withdrawal</span>
            </router-link>
          </div>
          <div class="col-3 p-0">
            <a :href="$asseturl+'Candy_Shop.apk'" class="linkColor">
                <i class="fa-solid fa-tablet-screen-button"></i>
              <span>Android app</span>
            </a>
          </div>
          <div class="col-3 p-0">
            <router-link :to="{name:'invite'}" class="linkColor">
                <i class="fa-solid fa-user-plus"></i>
              <span>Invite Friends</span>
            </router-link>
          </div>
        </div>
      </div>
    </section>




    <section id="announcement">
      <div class="container-fluid">
        <!-- <h3>IDG ID (ID:30369)</h3> -->
        <div class="row">


          <div class="col-12 p-0" v-for="plan in row" :key="plan.id">
            <div class="task me-1 mb-2">
              <a href="javascript:void(0)" class="plansdesign">
                <h4 class="planPack"  style="width:20%" >{{ plan.name }}</h4>
                <div class="vip-area planPack" style="width:40%">

                  <img class="lock" v-if="plan.id==user.user.plan_id" :src="$asseturl + 'frontend/img/unlock.png'" alt="unlocked" />

                  <img class="lock" v-else :src="$asseturl + 'frontend/img/lock.png'" alt="unlocked" />

                  <p>{{ plan.totalorder }} Orders</p>
                  <img
                    class="vip"
                    :src="$asseturl + 'frontend/img/vipLogo.png'"
                    alt="vip"
                  />
                </div>
                <span class="planPack"  style="width:40%">কমিশন রেট {{ parseFloat(plan.comission_rate*plan.totalorder).toFixed(2) }}% ({{ plan.start_balance }}TK-{{ plan.end_balance }}TK)</span>
              </a>
            </div>
          </div>


          <div class="col-md-12">
            <!-- <h3 class="text-center">Our Partners</h3> -->
            <!-- <hr> -->
            <img width="100%" :src="$asseturl+'frontend/img/partners.jpeg'" alt="">
          </div>

        </div>
      </div>
    </section>


    <div class="notice" v-if="notice">

<p> <h3>Welcome</h3>
    <br>
    <p v-html="settings.notice"></p>
</p>

        <button class="closebtn" @click="closeNotice">Close</button>
    </div>




  </div>
</template>

<script>


export default {
    created() {
        if(localStorage.getItem('notice')==1){
             this.notice = false
        }
        this.getplans()
        // console.log(this.slider.length)
        var indexx = 1;
        this.slideimage = this.slider[0]
        setInterval(() => {
            if(indexx===this.slider.length)indexx = 0;
            // console.log(indexx);
            this.slideimage = this.slider[indexx]
            indexx++
        }, 5000);

    },
    data(){
        return {
            settings:{},
            row:{},
            notice:true,
            slideimage:'',
            user:{
                user:{}
            },
            slider:[
            // this.$asseturl+'frontend/img/Daily-Task-Commisson-Chart.png',
            // this.$asseturl+'frontend/img/Refar-Deposit-Bonus.png',
            // this.$asseturl+'frontend/img/Refar-Task-income.png',
            // this.$asseturl+'frontend/img/Self-Deposit.png'
            ]
        }
    },
    methods: {


        closeNotice(){
            this.notice = false

        localStorage.setItem('notice',1)

        },

       async getplans(){

            var res = await this.callApi('get',`/api/admin/plan`,[])
            this.row = res.data

            var resN = await this.callApi('get',`/api/admin/setting`,[])
              this.settings = resN.data

              if(resN.data.slide1)this.slider.push(resN.data.slide1);
            if(resN.data.slide2)this.slider.push(resN.data.slide2);
            if(resN.data.slide3)this.slider.push(resN.data.slide3);
            if(resN.data.slide4)this.slider.push(resN.data.slide4);



             var id = localStorage.getItem('userid');
            var results = await this.callApi('get', `/api/admin/user/${id}`, []);
            this.user = results.data;


        }
    },

}
</script>
<style>
#marquee {
  margin: 24px 0;
}

    .reImage {
        padding: 6px;
background: #e1e1e1;
box-shadow: 0px 0px 10px 0px #0000008c;
    }
    .notice {
    width: 340px;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    background: #f0f0f0;
    padding: 52px 11px;
    z-index: 99;
    border-radius: 10px;
    text-align: center;
}

.closebtn {
  position: absolute;
  bottom: 7px;
  background: transparent;
  border: 2px solid #7683aa;
  border-radius: 6px;
  right: 23px;
}
.plansdesign{
    display: flex;
justify-content: space-between;
}

/* .planPack {
  width: 30%;
} */

a.linkColor i {
    font-size: 35px;
    color: #D8255F;
}

</style>
