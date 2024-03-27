<template>
  <section class="comments">
    <div class="comments__header">
      <h1 class="comments__title">Comments ({{ comments.length }})</h1>
      <button class="comments__button" @click="showAddCommentForm = !showAddCommentForm" v-if="!showAddCommentForm">{{ showAddCommentForm ? "" : "Add Comment" }}</button>
      <div class="comments__form-container" v-if="showAddCommentForm">
        <form class="form comments__form" @submit.prevent="addComment">
          <button class="comments__close-button" @click="showAddCommentForm = false">Close</button>
          <label class="form__label">
            <input class="form__input" type="text" v-model="newComment.author" placeholder="Author" />
          </label>
          <label class="form__label">
            <textarea class="form__input-text" v-model="newComment.text" rows="3" placeholder="Add a comment"></textarea>
          </label>
          <label class="form__label-reaction">
            <input class="form__radio" type="radio" name="reaction" v-model="newComment.reaction" value="1"
              aria-label="positive reaction">
            <svg width="24" height="24" viewBox="0 0 1024 1024" fill="currentColor" class="icon" version="1.1"
              xmlns="http://www.w3.org/2000/svg">
              <path
                d="M324.8 440c34.4 0 62.4-28 62.4-62.4s-28-62.4-62.4-62.4-62.4 28-62.4 62.4 28 62.4 62.4 62.4z m374.4 0c34.4 0 62.4-28 62.4-62.4s-28-62.4-62.4-62.4-62.4 28-62.4 62.4 28 62.4 62.4 62.4zM340 709.6C384 744 440.8 764.8 512 764.8s128-20.8 172-55.2c26.4-21.6 42.4-42.4 50.4-58.4 6.4-12 0.8-27.2-11.2-33.6s-27.2-0.8-33.6 11.2c-0.8 1.6-3.2 6.4-8 12-7.2 10.4-17.6 20-28.8 29.6-34.4 28-80.8 44.8-140.8 44.8s-105.6-16.8-140.8-44.8c-12-9.6-21.6-20-28.8-29.6-4-5.6-7.2-9.6-8-12-6.4-12-20.8-17.6-33.6-11.2s-17.6 20.8-11.2 33.6c8 16 24 36.8 50.4 58.4z"
                fill="currentColor" />
              <path
                d="M512 1010.4c-276.8 0-502.4-225.6-502.4-502.4S235.2 5.6 512 5.6s502.4 225.6 502.4 502.4-225.6 502.4-502.4 502.4zM512 53.6C261.6 53.6 57.6 257.6 57.6 508s204 454.4 454.4 454.4 454.4-204 454.4-454.4S762.4 53.6 512 53.6z"
                fill="currentColor" />
            </svg>
          </label>
          <label class="form__label-reaction">
            <input class="form__radio" type="radio" name="reaction" v-model="newComment.reaction" value="0"
              aria-label="neutral reaction">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
              <path
                d="M9 11C9.55228 11 10 10.5523 10 10C10 9.44772 9.55228 9 9 9C8.44772 9 8 9.44772 8 10C8 10.5523 8.44772 11 9 11Z"
                fill="currentColor" />
              <path
                d="M9 15C8.44772 15 8 15.4477 8 16C8 16.5523 8.44772 17 9 17H15C15.5523 17 16 16.5523 16 16C16 15.4477 15.5523 15 15 15H9Z"
                fill="currentColor" />
              <path
                d="M16 10C16 10.5523 15.5523 11 15 11C14.4477 11 14 10.5523 14 10C14 9.44772 14.4477 9 15 9C15.5523 9 16 9.44772 16 10Z"
                fill="currentColor" />
              <path fill-rule="evenodd" clip-rule="evenodd"
                d="M22 12C22 17.5228 17.5228 22 12 22C6.47715 22 2 17.5228 2 12C2 6.47715 6.47715 2 12 2C17.5228 2 22 6.47715 22 12ZM20 12C20 16.4183 16.4183 20 12 20C7.58172 20 4 16.4183 4 12C4 7.58172 7.58172 4 12 4C16.4183 4 20 7.58172 20 12Z"
                fill="currentColor" />
            </svg>
          </label>
          <label class="form__label-reaction">
            <input class="form__radio" type="radio" name="reaction" v-model="newComment.reaction" value="-1"
              aria-label="negative reaction">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
              <path
                d="M9 11C9.55228 11 10 10.5523 10 10C10 9.44772 9.55228 9 9 9C8.44772 9 8 9.44772 8 10C8 10.5523 8.44772 11 9 11Z"
                fill="currentColor" />
              <path
                d="M14 17C14 15.8954 13.1046 15 12 15C10.8954 15 10 15.8954 10 17H8C8 14.7909 9.79086 13 12 13C14.2091 13 16 14.7909 16 17H14Z"
                fill="currentColor" />
              <path
                d="M16 10C16 10.5523 15.5523 11 15 11C14.4477 11 14 10.5523 14 10C14 9.44772 14.4477 9 15 9C15.5523 9 16 9.44772 16 10Z"
                fill="currentColor" />
              <path fill-rule="evenodd" clip-rule="evenodd"
                d="M22 12C22 17.5228 17.5228 22 12 22C6.47715 22 2 17.5228 2 12C2 6.47715 6.47715 2 12 2C17.5228 2 22 6.47715 22 12ZM20 12C20 16.4183 16.4183 20 12 20C7.58172 20 4 16.4183 4 12C4 7.58172 7.58172 4 12 4C16.4183 4 20 7.58172 20 12Z"
                fill="currentColor" />
            </svg>
          </label>
          <div class="form__switch-container">
            <p class="form__switch-text">Adding a comment in real time:</p>
          <label class="form__switch" for="switch" aria-label="Добавление в реальном времени:">
            <input class="form__checkbox" type="checkbox" id="switch" v-model="realtimeSwitch"
              @change="toggleRealtimeComments" />
            <span class="form__slider slider"></span>
          </label>
        </div>
          <button :disabled="isFormEmpty" class="form__button">Add Comment</button>
          <p class="form__warning" v-if="isFormEmpty">Fill out the form completely</p>
        </form>
      </div>
    </div>
    <div class="comments__list">
      <Comment v-for="comment in parentComments" :key="comment.id" :comment="comment" :getReplies="getReplies" />
    </div>
  </section>
</template>

<script>
import Comment from "./components/Comment.vue";

export default {
  components: {
    Comment,
  },
  data() {
    return {
      comments: [],
      parentComments: [],
      realtimeSwitch: true,
      stream: null,
      showAddCommentForm: false,
      newComment: {
        author: "",
        text: "",
        reaction: 0,
        parentId: null,
      },
    };
  },
  computed: {
    isFormEmpty() {
      return !(this.newComment.author && this.newComment.text);
    }
  },
  methods: {
    getReplies(commentId) {
      return this.comments.filter((c) => c.parentId === commentId);
    },
    fetchComments() {
      fetch("http://194.67.93.117:80/comments", {
        headers: {
          "Content-Type": "application/json",
          Username: "K0rzet",
        },
      })
        .then((res) => res.json())
        .then((data) => {
          this.comments = data.reverse();
          this.parentComments = this.comments.filter((c) => c.parentId === null);
        });
    },
    commentExists(commentId) {
      return this.comments.some((c) => c.id === commentId);
    },
    initStream() {
      this.stream = new EventSource("http://194.67.93.117:80/comments/stream");
      this.stream.onmessage = (e) => {
        if (this.realtimeSwitch) {
          const newComment = JSON.parse(e.data);
          if (!this.commentExists(newComment.id)) {
            this.comments.push(newComment);
            if (!newComment.parentId) {
              this.parentComments.push(newComment);
            }
          }
        }
      };
    },
    toggleRealtimeComments() {
      if (this.realtimeSwitch) {
        this.initStream();
      } else {
        this.stream.close();
      }
    },
    addComment() {
      fetch("http://194.67.93.117:80/comments", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Username: "K0rzet",
        },
        body: JSON.stringify(this.newComment),
      })
        .then((res) => res.json())
        .then(() => {
          this.newComment.reaction = 0;
          this.newComment.author = "";
          this.newComment.text = "";
          this.showAddCommentForm = false;
        });
    },
  },
  mounted() {
    this.fetchComments();
    this.initStream();
    document.documentElement.lang = 'en';
  },
};  
</script>

<style>

.comments__form-container {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  overflow: auto;
  background-color: rgba(0, 0, 0, .7);
  padding: 10px;
}

.comments__form {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  background-color: rgb(255, 255, 255);
  border: 2px solid #9087f6;
  min-height: 60%;
  max-width: 100%;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  border-radius: 50px;
  padding: 5px;
  margin: auto;
}


.form {
  max-width: 300px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

.form__warning {
  color: #faaf90;
}

.form__radio:checked+svg {
  color: #9087f6;
}

.comments {
  max-width: 600px;
  margin: 0 auto;
}
.comments__button,
.comments__close-button {
  background-color: #f8dc93;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  border-radius: 4px;
  font-size: 16px;
  transition: background-color 0.3s ease;
  margin-left: 5px;
}

.comments__header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 0;
  gap: 20px;
  max-width: 100%;
  flex-direction: column;
}

.form__switch-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.form__switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.form__switch .form__checkbox {
  opacity: 0;
  width: 0;
  height: 0;
}

.form__switch .form__checkbox:focus+.form__slider {
  background-color: #b9e192;
}

.form__slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  transition: 0.4s;
}



.form__slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  transition: 0.4s;
}

.form__checkbox:checked+.form__slider {
  background-color: #f8dc93;
}

.form__checkbox:checked+.form__slider:before {
  transform: translateX(26px);
}

.comments__form {
  margin-top: 1rem;
}

.comments__form textarea {
  max-width: 80%;
  resize: vertical;
  padding: 0.5rem;
  margin-bottom: 0.5rem;
}

.comments__form button {
  padding: 0.5rem 1rem;
}

.form__button {
  background-color: #f8dc93;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  border-radius: 4px;
  font-size: 16px;
  transition: background-color 0.3s ease;
  max-width: 80%;
}

.form__button:disabled {
  background-color: #acacac;
  cursor: not-allowed;
}

.form__button:hover {
  background-color: #2d2d2d;
}

.form__input,
.form__input-text {
  max-width: 80%;
  padding: 10px;
  border-width: 2px;
  border-style: solid;
  border-color: #ddd;
  margin-bottom: 10px;
  font-size: 16px;
  line-height: 1.5;
  color: #333;
}

.form__input:focus,
.form__input-text:focus {
  border-color: #f8dc93;
  outline: none;
}

.form__radio {
  display: none;
}

.form__radio+svg {
  fill: #ddd;
  cursor: pointer;
}

.form__radio:checked+svg {
  fill: #f8dc93;
}

@media screen and (min-width: 375px) {
  .comments {
    max-width: 600px;
  }
}

@media screen and (min-width: 576px) {
  .comments__header {
    flex-direction: row;
  }
}

@media screen and (min-width: 768px) {
  .comments {
    max-width: 800px;
  }
}

@media screen and (min-width: 1024px) {
  .comments {
    max-width: 1000px;
  }
}

@media screen and (min-width: 1440px) {
  .comments {
    max-width: 1200px;
  }
}

@media screen and (min-width: 2560px) {
  .comments {
    max-width: 1400px;
  }
}
</style>