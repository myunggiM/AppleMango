<template>
    <div class="review-table">
        <!--리뷰 헤더 시작-->
        <div class="d-flex justify-space-between mb-2">
            <h1 class="text-left">식당 리뷰들</h1>

            <!--params 안에 동적라우팅 변수 추후에 변경 요망-->
            <!--리뷰 작성페이지 링크 시작-->
            <div class="my-auto">
                <router-link v-bind:to="{ name:'ReviewForm', params: {rid:1} }" style="text-decoration:none">
                    <v-btn color="#E0E0E0" class="font-weight-bold">리뷰 작성하러 가기!</v-btn>
                </router-link>
            </div>
            <!--리뷰 작성페이지 링크 종료-->
        </div>
        <!--리뷰 헤더 종료-->

        <!--리뷰 grid 시작-->
        <v-container
        class="rounded mx-0 mx-auto mb-2"
        style="background-color:#EFEBE9"
        v-for="review in reviews" v-bind:key="review.id">
          <v-row class="ma-1">
              <v-col cols="4">
                  <v-img src="https://images.pexels.com/photos/704569/pexels-photo-704569.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940"
                  contain aspect-ratio="1.5"></v-img>
              </v-col>
              <v-col cols="8" class="text-left d-flex flex-column">
                  <h1>{{ review.title }}</h1>
                  <div class="d-flex">
                      <div class="mr-2">평점: 
                          <v-rating style="display:inline" 
                          readonly v-model="review.star" color="orange" small dense background-color="orange">
                          </v-rating>
                      </div>
                      <div class="mr-2">작성자: {{ review.userId }}</div>
                      <!-- <div>작성일: {{ review.createdDate[0] + review.createdDate[1] }}</div> -->
                  </div>
                  <p>
                      {{ review.description }}  
                  </p>
                  <div fixed class="d-flex justify-space-between mt-auto">
                      <p>#해시태그 #여기들어가야함</p>
                      <v-btn @click="commentToShow = review.reviewId; commentSwitch = !commentSwitch"
                      x-small>
                        <!-- <span v-if="commentSwitch === true">댓글 닫기</span> -->
                        <span v-if="toggleComment(review.reviewId)" class="font-weight-bold">댓글 닫기</span>
                        <span v-else class="font-weight-bold">댓글 보기</span>
                      </v-btn>
                  </div>
              </v-col>
              <!-- <v-col v-if="commentToShow === review.reviewId" style="background-color:white"> -->
            <v-expand-transition>
              <v-col v-if="toggleComment(review.reviewId)" style="background-color:white">
                <!-- <comment-form v-on:create="registerComment" v-bind:reid="review.reviewId"></comment-form> -->
                <comment-form v-on:create="refresh" v-bind:reid="review.reviewId"></comment-form>
                <p v-if="filteredComments.length === 0">댓글이 아직 없습니다 ㅠㅠ</p>
                <h4 v-else class="text-left mb-2">댓글 목록</h4>
                <v-card v-for="comment in filteredComments" :key="comment.id" class="text-left mb-1">
                    <v-card-subtitle class="font-weight-bold">작성자: {{ comment.userId }}</v-card-subtitle>
                    <v-card-text>{{ comment.content }}</v-card-text>
                </v-card>
              </v-col>
            </v-expand-transition>
          </v-row>
        </v-container>
        <!--리뷰 grid 종료-->
    </div>
</template>

<script>
import axios from 'axios'
import CommentForm from '../review/CommentForm'
//import ReviewList from '../review/ReviewList.vue'

//local
// const BACKEND_URL = "http://localhost:8080/"
const BACKEND_URL = "http://i3a503.p.ssafy.io:8080/"

export default {
    name: "Review",
    components: {
      CommentForm,
      //ReviewList
    },
    data(){
        return {
            reviews: [],
            comments: [],
            filteredComments: [],
            commentToShow:'',
            commentSwitch: false,
            isLoggedIn: '',
        }
    },
    methods:{
        registerComment: function(commentData){
            axios.post(`${BACKEND_URL}comment/new`,commentData)
            .then(response => {
                console.log(commentData)
                console.log(response.data)
                this.comments.unshift(response.data) //새로운댓글 배열에 추가후 배열의 처음으로 이동.
            })
        },
        toggleComment: function(reviewId){
            if (this.commentSwitch === true && this.commentToShow === reviewId){
                return true
            }
        },
        filterComment: function(){
            this.comment = this.comment.filter(function(v){
                console.log(this.commentToShow)
                return v === this.commentToShow
            })
        },
        // getCookie: function(){
        //     if(this.$cookies.get('auth-token')){
        //         console.log(this.$cookies.get('auth-token'))
        //         return this.isLoggedIn = true
        //     }

        // }
        refresh: function(data){
            this.comments.unshift(data)
        }
    },
    mounted(){
        axios.get(`${BACKEND_URL}review`)
        .then(response => {
            this.reviews = response.data;
            console.log(response)
        })
        axios.get(`${BACKEND_URL}comment/all`)
        .then(response => {
            this.comments = response.data;
            console.log(response)
        })
    },
    watch: {
        commentToShow: function(){
            this.filteredComments = this.comments.filter(comment => {
                return comment.reviewId === this.commentToShow
            })
        },
        comments: function(){
            this.filteredComments = this.comments.filter(comment => {
                return comment.reviewId === this.commentToShow
            })
        },
    }

}
</script>

<style>
.review-table{
    margin: 0px 100px;
}
</style>