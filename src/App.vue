<template>
  <div id="activityApp">
    <nav class="navbar is-white topNav">
      <div class="container">
        <div class="navbar-brand">
          <h1>Activity Planner</h1>
        </div>
      </div>
    </nav>
    <nav class="navbar is-white">
      <div class="container">
        <div class="navbar-menu">
          <div class="navbar-start">
            <a class="navbar-item is-active" href="#">Newest</a>
            <a class="navbar-item" href="#">In Progress</a>
            <a class="navbar-item" href="#">Finished</a>
          </div>
        </div>
      </div>
    </nav>
    <section class="container">
      <div class="columns">
        <div class="column is-3">
          <a
            v-if="isNewButtonDisplayed"
            class="button is-primary is-block is-alt is-large"
            href="#"
            @click="openForm"
            >New Activity</a
          >
          <div v-if="isFormDisplayed" class="create-form">
            <h2>Create Activity</h2>
            <form>
              <div class="field">
                <label class="label">Title</label>
                <div class="control">
                  <input
                    v-model="newActivity.title"
                    class="input"
                    type="text"
                    placeholder="Read a Book"
                  />
                </div>
              </div>
              <div class="field">
                <label class="label">Notes</label>
                <div class="control">
                  <textarea
                    class="textarea"
                    placeholder="Textarea"
                    v-model="newActivity.notes"
                  ></textarea>
                </div>
              </div>
              <div class="field is-grouped">
                <div class="control">
                  <button class="button is-link">Create Goal</button>
                </div>
                <div class="control">
                  <button class="button is-text" @click="closeForm">
                    Cancel
                  </button>
                </div>
              </div>
            </form>
          </div>
        </div>
        <div class="column is-9">
          <div class="box content">
            <ActivityItem
              v-for="activity in activities"
              :activity="activity"
              :key="activity.id"
            ></ActivityItem>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import ActivityItem from "@/components/ActivityItem";
import {fetchActivities} from '@/api/index';

export default {
  name: "App",
  components: { ActivityItem },
  data() {
    return {
      message: "Hello Vue!",
      titleMessage: "Title Message Vue!!!!!",
      isTextDisplayed: true,
      isFormDisplayed: false,
      isNewButtonDisplayed: true,
      newActivity: {
        title: "",
        notes: "",
      },
      items: { 1: { name: "Diego" }, 2: { name: "Zoraya" } },
      user: {
        name: "Filip Jerga",
        id: "-Aj34jknvncx98812",
      },
      activities: {},
      categories: {
        1546969049: { text: "books" },
        1546969225: { text: "movies" },
      }
    };
  },
  beforeCreate() {
    console.log("beforeCreate called!");
  },
  created() {
    this.activities = fetchActivities();
  },
  beforeMount() {
    console.log("beforeMount called!");
  },
  mounted() {
    console.log("mounted called!");
  },
  updated() {
    console.log("updated called!");
  },
  beforeDestroyed() {
    console.log("beforeDestroyed called!");
  },
  destroyed() {
    console.log("destroyed called!");
  },
  methods: {
    toggleTextDisplay: function () {
      this.isTextDisplayed = !this.isTextDisplayed;
    },
    openForm: function () {
      this.isNewButtonDisplayed = false;
      this.isFormDisplayed = true;
    },
    closeForm: function () {
      this.isFormDisplayed = false;
      this.isNewButtonDisplayed = true;
    },
  },
};
</script>

<style>
#activityApp {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

html,
body {
  font-family: "Open Sans", serif;
  background: #f2f6fa;
}
footer {
  background-color: #f2f6fa !important;
}
.topNav {
  border-top: 5px solid #3498db;
}
.topNav .container {
  border-bottom: 1px solid #e6eaee;
}
.container .columns {
  margin: 3rem 0;
}
.navbar-menu .navbar-item {
  padding: 0 2rem;
}
aside.menu {
  padding-top: 3rem;
}
aside.menu .menu-list {
  line-height: 1.5;
}
aside.menu .menu-label {
  padding-left: 10px;
  font-weight: 700;
}
.button.is-primary.is-alt {
  background: #00c6ff;
  background: -webkit-linear-gradient(to bottom, #0072ff, #00c6ff);
  background: linear-gradient(to bottom, #0072ff, #00c6ff);
  font-weight: 700;
  font-size: 14px;
  height: 3rem;
  line-height: 2.8;
}
.media-left img {
  border-radius: 50%;
}
.media-content p {
  font-size: 14px;
  line-height: 2.3;
  font-weight: 700;
  color: #8f99a3;
}
article.post {
  margin: 1rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid #e6eaee;
}
article.post:last-child {
  padding-bottom: 0;
  border-bottom: none;
}
.menu-list li {
  padding: 5px;
}

.navbar-brand > h1 {
  font-size: 31px;
  padding: 20px;
}

.example-wrapper {
  margin-left: 30px;
}
</style>
