<script setup lang="ts">
import { ref } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faUser, faCodePullRequest, faEnvelope } from '@fortawesome/free-solid-svg-icons'

const term = ref(localStorage.getItem('term') || '')

const goto = (url: string) => (document.location.href = url)
const ddg = () => 'https://duckduckgo.com/?q=' + term.value

const onEnter = () => goto(ddg())
const onAltEnter = () => goto('https://' + term.value)
const onCtrlEnter = () => window.open(ddg(), '_blank')

window.onbeforeunload = () => localStorage.setItem('term', term.value)
</script>

<template>
  <header>
    <github>
      <a href="https://github.com/notifications">
        <FontAwesomeIcon :icon="faEnvelope" />
      </a>
      <a href="https://github.com/Jamim">
        <FontAwesomeIcon :icon="faUser" />
      </a>
      <a :href="'https://github.com/pulls?q=is:pr+is:open+author:@me+sort:updated-desc+' + term">
        <FontAwesomeIcon :icon="faCodePullRequest" />
      </a>
    </github>
  </header>
  <query>
    <input
      id="term"
      v-model="term"
      v-on:keyup.exact.enter="onEnter"
      v-on:keyup.alt.enter="onAltEnter"
      v-on:keyup.ctrl.enter="onCtrlEnter"
      autofocus
    />
  </query>
  <links>
    <div id="gentoo" class="group-wrapper">
      <gentoo class="group">
        <span>gentoo</span>
        <a :href="'https://bugs.gentoo.org/buglist.cgi?quicksearch=' + term">bugs</a>
        <a :href="'https://github.com/gentoo/gentoo/pulls?q=is:pr+is:open+' + term">prs</a>
        <a :href="'https://gpo.zugaina.org/Search?search=' + term">gpo</a>
      </gentoo>
    </div>
    <packages class="group">
      <span>packages</span>
      <pypi class="subgroup">
        <a :href="'https://pypi.org/project/' + term + '/'">pypi</a>
        <a :href="'https://pypistats.org/packages/' + term" class="sub">stats</a>
        <a :href="'https://www.pepy.tech/projects/' + term" class="sub">pepy</a>
      </pypi>
      <a :href="'https://repology.org/project/' + term + '/versions'">repology</a>
    </packages>
    <div class="group-wrapper">
      <search class="group">
        <span>search</span>
        <a :href="'https://duckduckgo.com/?q=' + term">🦆🦆🐾</a>
        <a :href="'https://www.google.com/search?q=' + term">google</a>
      </search>
    </div>
  </links>
</template>
