<template>
  <!-- 특정 웹툰의 화수를 보여주는 컴포넌트 입니다.
    상태 관리를 통해 수정 가능합니다.
 -->
  <v-container class="webtoon_round">
    <!-- 가장 기본적인 웹툰 화수를 표현하는 컴포넌트 -->
    <v-card
      v-if="webtoon_round_State == 0"
      v-scroll.self="onScroll"
      class="overflow-y-auto"
      max-height="400"
    >
      <v-banner class="justify-center text-h5 font-weight-light" sticky>
        최신화부터 | 1화부터
        <span class="font-weight-bold" v-text="scrollInvoked"></span>
      </v-banner>

      <v-card-text>
        <div :key="n" class="mb-4">
          <v-row v-for="(toon, index) in webtoon" :key="index">
            <v-col cols="3"
              ><router-link to="/viewer"
                ><v-img :src="toon.url" width="150" height="150"/></router-link
            ></v-col>
            <v-col cols="9"
              ><v-card>{{ toon.round }} | {{ toon.date }}</v-card></v-col
            >
          </v-row>
        </div>
      </v-card-text>
    </v-card>
    <!--  
            작가 사용자에게 보이는 작품 홈 페이지 에피소드 컴포넌트
            
            수정 버튼이 있으며 상단 EDIT 클릭시 에피소드 작성 페이지로 이동

            에피소드 옆 연필 버튼 클릭시 에피소드 수정 페이지 모달 생성
            
            -->
    <v-card
      v-if="webtoon_round_State == 1"
      v-scroll.self="onScroll"
      class="overflow-y-auto"
      max-height="400"
    >
      <v-banner class="justify-center font-weight-light text-end" sticky>
        최신화부터 | 1화부터
      </v-banner>

      <router-link to="/EDIT_EPISODE" class="ma-2">
        <v-btn block height="100">
          <v-icon>
            mdi-pencil
          </v-icon>
          Edit
        </v-btn>
      </router-link>
      <v-card-text>
        <div :key="n" class="mb-4">
          <v-row v-for="(toon, index) in webtoon" :key="index">
            <v-btn class="col-1" dark small color="green" height="150">
              <v-icon dark>mdi-pencil</v-icon></v-btn
            >
            <v-col class="col-3"
              ><v-img :src="toon.url" width="150" height="150"
            /></v-col>
            <v-col class="col-7"
              ><v-card>{{ toon.round }} | {{ toon.date }}</v-card></v-col
            >
          </v-row>
        </div>
      </v-card-text>
    </v-card>
    <!--  
        승인 페이지 에피소드 컴포넌트
        
        올린 에피소드 상태 확인

        상태는 심사 중 / 반려 / 승인 이 있음
        
        -->
    <v-card fluid v-if="webtoon_round_State == 2">
      <v-row v-for="(toon, index) in webtoon" :key="index">
        <v-col class="col-3"
          ><v-img :src="toon.url" width="150" height="150"
        /></v-col>
        <v-col class="col-7"
          ><v-card>{{ toon.round }} | {{ toon.date }}</v-card></v-col
        >
        <v-col class="col-1">
          <v-flex xs1>
            <v-dialog v-model="dialog" width="500">
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  class="col-1"
                  dark
                  small
                  color="green"
                  height="150"
                  v-bind="attrs"
                  v-on="on"
                  >{{ toon.state }}</v-btn
                >
              </template>

              <v-card>
                <v-card-title class="text-h5 grey lighten-2">
                  작품 반려 사유
                </v-card-title>
                <v-card-text height="40"> 사유 <br />작품 중복 </v-card-text>
                <v-divider />
                <v-spacer></v-spacer>
                <v-btn block color="primary" text @click="dialog = false">
                  확인
                </v-btn>
              </v-card>
            </v-dialog>
          </v-flex>
        </v-col>
      </v-row>
    </v-card>
  </v-container>
</template>
<script>
export default {
  name: "",
  components: {},
  props: ["webtoon_round_State"],
  data() {
    return {
      webtoon: [
        {
          url: require("../img/nft2.png"),
          round: "3화",
          date: "2021-10-13",
          state: "승인완료",
        },
        {
          url: require("../img/nft2.png"),
          round: "2화",
          date: "2021-10-6",
          state: "반려중",
        },
        {
          url: require("../img/nft2.png"),
          round: "1화",
          date: "2021-10-1",
          state: "승인대기중",
        },
      ],
    };
  },
  setup() {},
  create() {},
  mounted() {},
  unmounted() {},
  methods: {},
};
</script>
<style scoped></style>
