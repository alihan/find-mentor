<template>
  <div>
    <div class="container">
      <h1>
        <a
          href="https://github.com/cagataycali/find-mentor"
          target="_blank"
        >Feel free to contribute!</a>
      </h1>
      <h2>Exactly this project is 0km.</h2>
      <h3>
        Every night & every deploy, the spread sheet will be parsed by GitHub
        actions, then generate this beauty.
      </h3>
      <hr>
      <h4>Mentors</h4>
      <ul class="persons">
        <li v-for="mentor in mentors" :key="mentor.slug" class="person">
          <b-avatar
            :src="fixProtocol(mentor.name, mentor.github)"
            size="6rem"
          />
          <NuxtLink :to="'/mentor/' + mentor.slug">
            <h3 class="name">
              {{ mentor.name }}
            </h3>
          </NuxtLink>
          <p class="head">
            Interests:
          </p>
          <p class="interestContent">
            {{ mentor.interests }}
          </p>
        </li>
      </ul>
      <hr>
      <h4>Mentees</h4>
      <ul class="persons">
        <li v-for="mentee in mentees" :key="mentee.slug" class="person">
          <b-avatar
            :src="fixProtocol(mentee.name, mentee.github)"
            size="6rem"
          />
          <NuxtLink :to="'/mentee/' + mentee.slug">
            <h3 class="name">
              {{ mentee.name }}
            </h3>
          </NuxtLink>
          <p class="head">
            Interest:
          </p>
          <p class="interestContent">
            {{ mentee.interests }}
          </p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData ({ $content, params }) {
    const mentees = await $content('mentees').fetch()
    const mentors = await $content('mentors').fetch()
    return { mentees, mentors }
  },
  methods: {
    fixProtocol (name, url) {
      if (!url) {
        url = 'https://ui-avatars.com/api/?name=' + name
        return url
      }
      return url
        ? 'https://' + url.replace(/https?:\/\//gi, '').replace(/\/$/gi, '') + '.png?size=200'
        : 'javascript:void(0)'
    }
  }
}
</script>
<style>
* {
  box-sizing: border-box;
}
.persons {
  list-style-type: none;
  width: 100%;
  display: flex;
  flex-wrap: wrap;
}
.person {
  width: 250px;
  height: 250px;
  align-items: start;
  text-align: center;
  border: 1px solid grey;
  border-radius: 4px;
  padding-top: 10px;
  margin: 20px 10px 0 0;
  overflow: hidden;
}
.name {
  font-size: 26px;
  color: chocolate;
}
.head {
  color: #1d2124;
  font-size: large;
  margin-bottom: 0;
  display: inline-flex;
}
.interestContent {
  display: -webkit-box;
  -webkit-line-clamp: 4;
  -webkit-box-orient: vertical;
  padding: 0 3px;
  overflow: hidden;
}
</style>
