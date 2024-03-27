<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div class="comments__comment comment" :style="{ backgroundColor: reactionColor }">
        <div class="comment__header">
            <p class="comment__title">{{ comment.author }}</p>
            <p class="comment__date">{{ formatDate(comment.createdAt) }}</p>
        </div>
        <p class="comment__text">{{ comment.text }}</p>
        <p class="comment__reaction">Reaction:
            <span class="comment__reaction-ico" v-if="comment.reaction == -1">
                <svg class="comment__icon" width="24" height="24" viewBox="0 0 24 24" fill="currentColor"
                    xmlns="http://www.w3.org/2000/svg">
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
            </span>
            <span class="comment__reaction-ico" v-else-if="comment.reaction == 0">
                <svg class="comment__icon" width="24" height="24" viewBox="0 0 24 24" fill="currentColor"
                    xmlns="http://www.w3.org/2000/svg">
                    <path
                        d="M9 11C9.55228 11 10 10.5523 10 10C10 9.44772 9.55228 9 9 9C8.44772 9 8 9.44772 8 10C8 1010.5523 8.44772 11 9 11Z"
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
            </span>
            <span class="comment__reaction-ico" v-else-if="comment.reaction == 1">
                <svg class="comment__icon" width="20px" height="20px" viewBox="0 0 1024 1024" fill="currentColor"
                    version="1.1" xmlns="http://www.w3.org/2000/svg">
                    <path
                        d="M324.8 440c34.4 0 62.4-28 62.4-62.4s-28-62.4-62.4-62.4-62.4 28-62.4 62.4 28 62.4 62.4 62.4z m374.4 0c34.4 0 62.4-28 62.4-62.4s-28-62.4-62.4-62.4-62.4 28-62.4 62.4 28 62.4 62.4 62.4zM340 709.6C384 744 440.8 764.8 512 764.8s128-20.8 172-55.2c26.4-21.6 42.4-42.4 50.4-58.4 6.4-12 0.8-27.2-11.2-33.6s-27.2-0.8-33.6 11.2c-0.8 1.6-3.2 6.4-8 12-7.2 10.4-17.6 20-28.8 29.6-34.428-80.8 44.8-140.8 44.8s-105.6-16.8-140.8-44.8c-12-9.6-21.6-20-28.8-29.6-4-5.6-7.2-9.6-8-12-6.4-12-20.8-17.6-33.6-11.2s-17.6 20.8-11.2 33.6c8 16 24 36.8 50.4 58.4z"
                        fill="currentColor" />
                    <path
                        d="M512 1010.4c-276.8 0-502.4-225.6-502.4-502.4S235.2 5.6 512 5.6s502.4 225.6 502.4 502.4-225.6 502.4-502.4 502.4zM512 53.6C261.6 53.6 57.6 257.6 57.6 508s204 454.4 454.4 454.4 454.4-204 454.4-454.4S762.4 53.6 512 53.6z"
                        fill="currentColor" />
                </svg>
            </span>
        </p>
        <p class="comment__text" v-if="replies.length > 0">Answers amount: {{ replies.length }}</p>
        <button class="comment__button" @click="expandReplies = !expandReplies">
            {{ expandReplies ? "Hide Replies" : "Show Replies" }} ({{ replies.length }})
        </button>
        <div v-if="expandReplies" class="comment__replies replies">
            <div v-for="reply in replies" :key="reply.id" class="replies__reply reply">
                <Comment :comment="reply" :getReplies="getReplies"></Comment>
            </div>  
        </div>
        <button class="comment__button" @click="showReplyForm = !showReplyForm">{{ showReplyForm ? "Hide Reply Form" : "Show Reply Form" }}</button>
        <div v-if="showReplyForm" class="comment__reply-form reply-form">
            <form class="form reply__form" @submit.prevent="addReply">
                <label class="form__label">
                    <input class="form__input" type="text" v-model="newReply.author" placeholder="Author" />
                </label>
                <label class="form__label">
                    <textarea class="form__input-text" v-model="newReply.text" rows="3"
                        placeholder="Add a reply"></textarea>
                </label>
                <label class="form__label-reaction">
                    <input class="form__radio" type="radio" name="reaction" v-model="newReply.reaction" value="1"
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
                    <input class="form__radio" type="radio" name="reaction" v-model="newReply.reaction" value="0"
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
                    <input class="form__radio" type="radio" name="reaction" v-model="newReply.reaction" value="-1"
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
                <button :disabled="isReplyFormEmpty" class="form__submit-button" type="submit">Submit Reply</button>
            </form>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        comment: {
            type: Object,
            required: true
        },
        getReplies: {
            type: Function,
            required: true
        }
    },
    data() {
        return {
            expandReplies: false,
            showReplyForm: false,
            newReply: {
                author: "",
                text: "",
                reaction: 0,
                parentId: null,
            },
        };
    },
    computed: {
        replies() {
            return this.getReplies(this.comment.id);
        },
        isReplyFormEmpty() {
            return !(this.newReply.author && this.newReply.text);
        },
        reactionColor() {
            const totalReaction = this.replies.reduce((acc, reply) => acc + parseInt(reply.reaction), 0);
            if (totalReaction < 0) {
                return "#faaf90";
            } else if (totalReaction > 0) {
                return "#b9e192";
            } else {
                return "white";
            }
        }
    },
    methods: {
        formatDate(dateString) {
            const date = new Date(dateString);
            return date.toLocaleTimeString() + ', ' + date.toLocaleDateString();
        },
        async addReply() {
            this.newReply.parentId = this.comment.id;
            const response = await fetch("http://194.67.93.117:80/comments", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    "Username": "K0rzet",
                },
                body: JSON.stringify(this.newReply),
            });

            if (response.ok) {
                const newComment = await response.json();
                this.$emit("addReply", newComment);
                this.newReply.author = "";
                this.newReply.text = "";
                this.newReply.reaction = 0;
                this.showReplyForm = false;
            }
        }
    }
};
</script>
  
<style>
.comment {
    border: 1px solid #000;
    padding: 1rem;
    margin-bottom: 1rem;
    word-wrap: break-word;
}

.comment__header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 0.5rem;
    gap: 20px;
}

@media screen and (min-width: 320px) {
    .comment__header {
        flex-direction: column;
    }
}

@media screen and (min-width: 768px) {
    .comment__header {
        flex-direction: row;
    }
}

.comment__date {
    font-size: 0.8em;
    color: #000;
}

.comment__button {
    background-color: #f8dc93;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    border-radius: 4px;
    font-size: 16px;
    transition: background-color 0.3s ease;
    margin-left: 5px;
    margin-top: 5px;
}

.comment__button:hover {
    background-color: #2d2d2d;
}

.comment__title {
    font-weight: 900;
    font-size: 24px;
}

.replies {
    margin-top: 1rem;
    padding-left: 1rem;
}

.reply {
    margin-bottom: 0.5rem;
}

.reply__form {
    margin-top: 10px;
    padding: 10px;
    max-width: 80%;
}

.reply-form input,
.reply-form textarea {
    width: 100%;
    resize: vertical;
    padding: 0.5rem;
    margin-bottom: 0.5rem;
}

.reply-form button {
    padding: 0.5rem 1rem;
}

.form__submit-button {
    background-color: #f8dc93;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    border-radius: 4px;
    font-size: 16px;
    transition: background-color 0.3s ease;
    margin-left: 5px;
}

.form__submit-button:hover {
    background-color: #f8d16d;
}

.form__submit-button:disabled {
    background-color: #acacac;
    cursor: not-allowed;
}
</style>
  