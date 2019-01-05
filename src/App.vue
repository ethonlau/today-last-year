<template>
  <div id="app">
    <template v-if="this.jump">
      <div class="loader"></div>
      <div class="text">回顾中…</div>
    </template>
    <template v-else>
      <img src="data:image/png;base64,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">
      <div class="text">抱歉，往年今日没有发日报</div>
      <button @click="nextDaily">换一篇</button>
    </template>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      lastYear: [
        "https://www.jianshu.com/p/882d1be34d35", //180101
        "https://www.jianshu.com/p/cfa15fe3f2d5", //180102
        "https://www.jianshu.com/p/b818e2b8eb30", //180103
        "https://www.jianshu.com/p/377b229c7af2", //180104
        "", //180105
        "https://www.jianshu.com/p/3e95f12b6f97", //180106
        "", //180107
        "https://www.jianshu.com/p/c7123f5e4bd2", //180108
        "https://www.jianshu.com/p/d871c5f34727", //180109
        "https://www.jianshu.com/p/93456b1e4bc7", //180110
        "https://www.jianshu.com/p/51f98e5e91ad", //180111
        "", //180112
        "https://www.jianshu.com/p/eb90a7398990", //180113
        "", //180114
        "https://www.jianshu.com/p/25d93c8d96f3", //180115
        "https://www.jianshu.com/p/8d7098444baa", //180116
        "https://www.jianshu.com/p/a04b674f37aa", //180117
        "https://www.jianshu.com/p/6cc4ac5421cb", //180118
        "", //180119
        "https://www.jianshu.com/p/0996381737bc", //180120
        "", //180121
        "https://www.jianshu.com/p/79c3ae2d1715", //180122
        "https://www.jianshu.com/p/a2aeabe4d972", //180123
        "https://www.jianshu.com/p/a99b9cc34b5a", //180124
        "https://www.jianshu.com/p/872a0c97d619", //180125
        "", //180126
        "https://www.jianshu.com/p/39ff0a101e5c", //180127
        "", //180128
        "https://www.jianshu.com/p/defa909e856d", //180129
        "", //180130
        "", //180131
        "https://www.jianshu.com/p/ae868e3e8c18", //180201
        "https://www.jianshu.com/p/9575b57e9dd3", //180202
        "", //180203
        "", //180204
        "https://www.jianshu.com/p/46c79150bdd7", //180205
        "https://www.jianshu.com/p/90499680b02a", //180206
        "https://www.jianshu.com/p/7b50c6b938db", //180207
        "", //180208
        "", //180209
        "", //180210
        "https://www.jianshu.com/p/3257d24c0a17", //180211
        "https://www.jianshu.com/p/5e6d6cc3cf85", //180212
        "https://www.jianshu.com/p/1c8d13cb5ed0", //180213
        "https://www.jianshu.com/p/2469f18bb0ac", //180214
        "https://www.jianshu.com/p/749c73b565ca", //180215
        "", //180216
        "", //180217
        "", //180218
        "", //180219
        "", //180220
        "https://www.jianshu.com/p/126c6749e56b", //180221
        "https://www.jianshu.com/p/27a9ac755c28", //180222
        "https://www.jianshu.com/p/2f44e37c6511", //180223
        "https://www.jianshu.com/p/c381cb3f074e", //180224
        "", //180225
        "https://www.jianshu.com/p/3373d5074a3b", //180226
        "https://www.jianshu.com/p/5f07d2a18fb7", //180227
        "https://www.jianshu.com/p/a7cdafd2e88f", //180228
        "https://www.jianshu.com/p/b52415bc6ad3", //180301
        "https://www.jianshu.com/p/a329c218a5c2", //180302
        "", //180303
        "", //180304
        "https://www.jianshu.com/p/ba78b873ffb1", //180305
        "https://www.jianshu.com/p/1cee639e58b4", //180306
        "https://www.jianshu.com/p/794962fd69ce", //180307
        "https://www.jianshu.com/p/1565946a2794", //180308
        "https://www.jianshu.com/p/3a836aff43d9", //180309
        "", //180310
        "", //180311
        "https://www.jianshu.com/p/6ae865f31316", //180312
        "https://www.jianshu.com/p/da94b74550fb", //180313
        "https://www.jianshu.com/p/b3d218a0b398", //180314
        "https://www.jianshu.com/p/894f03150f62", //180315
        "", //180316
        "https://www.jianshu.com/p/27fd402031cb", //180317
        "", //180318
        "https://www.jianshu.com/p/382e2cfed174", //180319
        "https://www.jianshu.com/p/b805c39a2a4b", //180320
        "https://www.jianshu.com/p/a507f9ff2317", //180321
        "https://www.jianshu.com/p/2470bdc37dad", //180322
        "https://www.jianshu.com/p/737a28662eb5", //180323
        "", //180324
        "", //180325
        "https://www.jianshu.com/p/2915f14e5941", //180326
        "https://www.jianshu.com/p/1a54f8752aac", //180327
        "https://www.jianshu.com/p/d7b17183d7cc", //180328
        "https://www.jianshu.com/p/688c3e5a080d", //180329
        "https://www.jianshu.com/p/a30e79e75a0b", //180330
        "", //180331
        "", //180401
        "https://www.jianshu.com/p/10aaa368d56d", //180402
        "https://www.jianshu.com/p/0d2b6c8b293d", //180403
        "https://www.jianshu.com/p/579e46daabfc", //180404
        "", //180405
        "", //180406
        "", //180407
        "https://www.jianshu.com/p/27074fee2310", //180408
        "", //180409
        "https://www.jianshu.com/p/d17c9b8c5447", //180410
        "https://www.jianshu.com/p/f024f342c692", //180411
        "https://www.jianshu.com/p/050778d546e4", //180412
        "", //180413
        "", //180414
        "", //180415
        "https://www.jianshu.com/p/de4eb8f33d70", //180416
        "https://www.jianshu.com/p/ec149678a866", //180417
        "https://www.jianshu.com/p/e37048b0f2cb", //180418
        "https://www.jianshu.com/p/adaef814e26f", //180419
        "https://www.jianshu.com/p/4aea626a3a50", //180420
        "", //180421
        "", //180422
        "https://www.jianshu.com/p/86610c5ef0bc", //180423
        "https://www.jianshu.com/p/965b056900ea", //180424
        "https://www.jianshu.com/p/95743c953ac6", //180425
        "https://www.jianshu.com/p/07e0e083a043", //180426
        "https://www.jianshu.com/p/558faecc233f", //180427
        "https://www.jianshu.com/p/a4ddbeaca0e9", //180428
        "", //180429
        "", //180430
        "", //180501
        "https://www.jianshu.com/p/f068db542a52", //180502
        "https://www.jianshu.com/p/3e4e27d870b7", //180503
        "https://www.jianshu.com/p/b95c279fa849", //180504
        "", //180505
        "", //180506
        "https://www.jianshu.com/p/422742e2b623", //180507
        "https://www.jianshu.com/p/0089fc5e6518", //180508
        "https://www.jianshu.com/p/30346f3be05b", //180509
        "https://www.jianshu.com/p/27e3fe9ae23d", //180510
        "https://www.jianshu.com/p/40a9befe335a", //180511
        "", //180512
        "", //180513
        "https://www.jianshu.com/p/f873c29543fb", //180514
        "https://www.jianshu.com/p/265b7e10891a", //180515
        "https://www.jianshu.com/p/417e7fe97f43", //180516
        "https://www.jianshu.com/p/ff4513cb7db6", //180517
        "https://www.jianshu.com/p/1e4470211021", //180518
        "", //180519
        "", //180520
        "https://www.jianshu.com/p/caf12d1b6448", //180521
        "https://www.jianshu.com/p/7a8bd31b2ac5", //180522
        "https://www.jianshu.com/p/ca213777a7c2", //180523
        "https://www.jianshu.com/p/bb2448129e2d", //180524
        "https://www.jianshu.com/p/893781d6bc7e", //180525
        "", //180526
        "", //180527
        "https://www.jianshu.com/p/1ae832fb25e5", //180528
        "https://www.jianshu.com/p/6f0347b1c3aa", //180529
        "", //180530
        "https://www.jianshu.com/p/deb1baa00b47", //180531
        "https://www.jianshu.com/p/fe3f79d2d82c", //180601
        "", //180602
        "", //180603
        "https://www.jianshu.com/p/cd2c1752776e", //180604
        "https://www.jianshu.com/p/13fdadb8c57a", //180605
        "https://www.jianshu.com/p/12ad882a50e4", //180606
        "https://www.jianshu.com/p/8ce5a153774f", //180607
        "https://www.jianshu.com/p/04f4b2bbcec0", //180608
        "", //180609
        "", //180610
        "https://www.jianshu.com/p/c5b4f34a9f9e", //180611
        "https://www.jianshu.com/p/dab836dba52f", //180612
        "https://www.jianshu.com/p/3a57324f900b", //180613
        "https://www.jianshu.com/p/179d2f134c08", //180614
        "", //180615
        "", //180616
        "", //180617
        "", //180618
        "https://www.jianshu.com/p/96d002c808ad", //180619
        "https://www.jianshu.com/p/920cf2692bbb", //180620
        "https://www.jianshu.com/p/e9dee803d558", //180621
        "https://www.jianshu.com/p/40a757d009d4", //180622
        "", //180623
        "", //180624
        "", //180625
        "https://www.jianshu.com/p/ff3c54437ca1", //180626
        "https://www.jianshu.com/p/be52319f72ed", //180627
        "https://www.jianshu.com/p/fca79a674926", //180628
        "", //180629
        "https://www.jianshu.com/p/b6f250bd88e5", //180630
        "", //180701
        "https://www.jianshu.com/p/e5436f2fdd24", //180702
        "https://www.jianshu.com/p/4a476d4444dc", //180703
        "https://www.jianshu.com/p/6a3ccc432f95", //180704
        "https://www.jianshu.com/p/d1fc0e57a19c", //180705
        "https://www.jianshu.com/p/bfac89749ecd", //180706
        "", //180707
        "", //180708
        "", //180709
        "https://www.jianshu.com/p/ad1298c09d07", //180710
        "https://www.jianshu.com/p/5a1b231dbfbf", //180711
        "https://www.jianshu.com/p/63229c8aefb8", //180712
        "", //180713
        "", //180714
        "", //180715
        "https://www.jianshu.com/p/000974d726fc", //180716
        "", //180717
        "https://www.jianshu.com/p/97ef54c320f8", //180718
        "", //180719
        "", //180720
        "", //180721
        "", //180722
        "https://www.jianshu.com/p/c8129e3bcc10", //180723
        "https://www.jianshu.com/p/e2c0ace9773b", //180724
        "https://www.jianshu.com/p/78f1709f7e8b", //180725
        "https://www.jianshu.com/p/a6771b862fa4", //180726
        "https://www.jianshu.com/p/eaecbf6646d0", //180727
        "", //180728
        "", //180729
        "https://www.jianshu.com/p/1610e09e05d5", //180730
        "https://www.jianshu.com/p/b2047c44d983", //180731
        "https://www.jianshu.com/p/b5370a3bdba3", //180801
        "https://www.jianshu.com/p/e544cdaa7e45", //180802
        "https://www.jianshu.com/p/33802ac9c145", //180803
        "", //180804
        "", //180805
        "https://www.jianshu.com/p/f7a22b1ba676", //180806
        "", //180807
        "https://www.jianshu.com/p/74961e8621b6", //180808
        "https://www.jianshu.com/p/d379f99b23fb", //180809
        "https://www.jianshu.com/p/f45a45c2c6af", //180810
        "", //180811
        "", //180812
        "https://www.jianshu.com/p/2c956d5b11c2", //180813
        "", //180814
        "https://www.jianshu.com/p/f29da81590aa", //180815
        "", //180816
        "https://www.jianshu.com/p/91f3a39197df", //180817
        "", //180818
        "", //180819
        "https://www.jianshu.com/p/3959ef1fd0ed", //180820
        "https://www.jianshu.com/p/9a1a94c88405", //180821
        "https://www.jianshu.com/p/0237c1fe7c5a", //180822
        "https://www.jianshu.com/p/810ae0cbb819", //180823
        "https://www.jianshu.com/p/66047f95feb4", //180824
        "", //180825
        "", //180826
        "https://www.jianshu.com/p/b920e044ff3f", //180827
        "https://www.jianshu.com/p/d8997d1427d3", //180828
        "https://www.jianshu.com/p/382f9d69692e", //180829
        "https://www.jianshu.com/p/960cc5dc371e", //180830
        "https://www.jianshu.com/p/5fad2b25d3f3", //180831
        "", //180901
        "", //180902
        "https://www.jianshu.com/p/c8b7c82500a2", //180903
        "https://www.jianshu.com/p/342b186acc6e", //180904
        "https://www.jianshu.com/p/344d2a250890", //180905
        "https://www.jianshu.com/p/1a2a6a0a9b62", //180906
        "", //180907
        "https://www.jianshu.com/p/3e98d817ebd8", //180908
        "", //180909
        "https://www.jianshu.com/p/dd64cb2f65e0", //180910
        "https://www.jianshu.com/p/58e981230b54", //180911
        "", //180912
        "https://www.jianshu.com/p/ec81a8a8a668", //180913
        "https://www.jianshu.com/p/428554980cf1", //180914
        "", //180915
        "", //180916
        "https://www.jianshu.com/p/bba6d1e348f8", //180917
        "https://www.jianshu.com/p/410ef9b89d65", //180918
        "https://www.jianshu.com/p/e7e314a39b58", //180919
        "https://www.jianshu.com/p/f13114e63c5f", //180920
        "https://www.jianshu.com/p/f9de6ae20ac2", //180921
        "", //180922
        "", //180923
        "", //180924
        "https://www.jianshu.com/p/629afc7b8e62", //180925
        "", //180926
        "https://www.jianshu.com/p/2692d32a949d", //180927
        "", //180928
        "https://www.jianshu.com/p/db004ad5c852", //180929
        "", //180930
        "", //181001
        "", //181002
        "https://www.jianshu.com/p/0ce39943ef1c", //181003
        "", //181004
        "", //181005
        "", //181006
        "", //181007
        "", //181008
        "https://www.jianshu.com/p/617f6b60d514", //181009
        "https://www.jianshu.com/p/057c3c04cc65", //181010
        "", //181011
        "", //181012
        "https://www.jianshu.com/p/8425024c9759", //181013
        "", //181014
        "", //181015
        "https://www.jianshu.com/p/3ee3d89c3332", //181016
        "https://www.jianshu.com/p/1e6eb3bd1259", //181017
        "https://www.jianshu.com/p/014813f790d3", //181018
        "https://www.jianshu.com/p/402ed11db0e0", //181019
        "", //181020
        "", //181021
        "https://www.jianshu.com/p/0207565fd7c4", //181022
        "https://www.jianshu.com/p/b9df0daa4c67", //181023
        "", //181024
        "https://www.jianshu.com/p/7271d513ce1d", //181025
        "https://www.jianshu.com/p/fb4d0d4a5216", //181026
        "", //181027
        "", //181028
        "https://www.jianshu.com/p/ace63a57834f", //181029
        "", //181030
        "https://www.jianshu.com/p/a98650acdbbc", //181031
        "", //181101
        "", //181102
        "", //181103
        "", //181104
        "https://www.jianshu.com/p/65bd77b3e8bf", //181105
        "", //181106
        "", //181107
        "https://www.jianshu.com/p/91c09d6a81f8", //181108
        "", //181109
        "https://www.jianshu.com/p/c465dbe682b3", //181110
        "", //181111
        "https://www.jianshu.com/p/fe03e47542f4", //181112
        "https://www.jianshu.com/p/b54cce05d069", //181113
        "https://www.jianshu.com/p/b1fe4f25326b", //181114
        "https://www.jianshu.com/p/f6b49630270d", //181115
        "https://www.jianshu.com/p/a331408c2f18", //181116
        "", //181117
        "", //181118
        "https://www.jianshu.com/p/79b73c156638", //181119
        "", //181120
        "https://www.jianshu.com/p/682375190c37", //181121
        "", //181122
        "", //181123
        "", //181124
        "", //181125
        "https://www.jianshu.com/p/415f9021266a", //181126
        "", //181127
        "https://www.jianshu.com/p/8c817ae6deb5", //181128
        "https://www.jianshu.com/p/973e3fac59cd", //181129
        "https://www.jianshu.com/p/20643f1b4533", //181130
        "", //181201
        "", //181202
        "https://www.jianshu.com/p/804efff22361", //181203
        "https://www.jianshu.com/p/84706f3b1e9a", //181204
        "https://www.jianshu.com/p/a43d50ff2777", //181205
        "https://www.jianshu.com/p/4b6e04db98b2", //181206
        "https://www.jianshu.com/p/3bb058154a14", //181207
        "", //181208
        "", //181209
        "https://www.jianshu.com/p/bf728ed14067", //181210
        "https://www.jianshu.com/p/ee7e74b4d487", //181211
        "https://www.jianshu.com/p/6f4df8377520", //181212
        "https://www.jianshu.com/p/46321b75c511", //181213
        "https://www.jianshu.com/p/fde4f05e29ea", //181214
        "", //181215
        "", //181216
        "https://www.jianshu.com/p/1a0a6a739dbe", //181217
        "https://www.jianshu.com/p/ad7bdd943bbe", //181218
        "https://www.jianshu.com/p/d1cc12946f8d", //181219
        "https://www.jianshu.com/p/a7c20b962783", //181220
        "https://www.jianshu.com/p/a3f8d1150b2f", //181221
        "https://www.jianshu.com/p/c18d905f2f65", //181222
        "", //181223
        "https://www.jianshu.com/p/69b2e5fd828d", //181224
        "https://www.jianshu.com/p/5c5d3945503b", //181225
        "https://www.jianshu.com/p/59f567bdaf0c", //181226
        "https://www.jianshu.com/p/2f8c042abaf0", //181227
        "https://www.jianshu.com/p/f30e2196ce09", //181228
        "https://mp.weixin.qq.com/s/lL_LNayaGqLIU_BI5P_xWw", //181229
        "", //181230
        "", //181231
      ],
    }
  },
  mounted () {
    this.$nextTick (() => {
      if (this.jump) {
        window.location = this.lastYear[this.today - 1]
      }
    })
  },
  computed: {
    today () {
      return Math.ceil(( new Date() - new Date(new Date().getFullYear().toString()))/(86400000))
    },
    jump () {
      if (this.lastYear[this.today - 1] === '') {
        return false
      } else {
        return true
      }
    }
  },
  methods: {
    nextDaily() {
      if (this.lastYear[this.today] !== '') {
        window.location = this.lastYear[this.today]
      } else if (this.lastYear[this.today + 1] !== '') {
        window.location = this.lastYear[this.today + 1]
      } else if (this.lastYear[this.today + 2] !== '') {
        window.location = this.lastYear[this.today + 2]
      } else if (this.lastYear[this.today + 3] !== '') {
        window.location = this.lastYear[this.today + 3]
      } else {
        //do nothing
      }
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-60%);
  width: 200px;

  .loader {
    margin: 0 auto;
    width: 20px;
    height: 20px;
    border: 3px solid #1aa0ff;
    border-left-color: transparent;
    border-radius: 50%;
    animation: rolling 1s infinite;

  }

  @keyframes rolling {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }

  .text {
    margin-top: 20px;
    font-size: 16px;
    color: #999;
  }

  img {
    width: 100px;
  }

  button {
    margin-top: 25px;
    padding: 4px 16px;
    border: 1px solid #1aa0ff;
    border-radius: 6px;
    color: #1aa0ff;
    background-color: transparent;
  }
}
</style>
