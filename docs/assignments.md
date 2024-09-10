---
layout: doc
---

<script setup>
  import {data as assignments} from './assignments/a.data';
  import { withBase } from 'vitepress';
</script>

# Assignments

<ul v-if="assignments.length > 0">
  <li v-for="a of assignments">
    <a :href="withBase(a.url)">{{ a.frontmatter.title }}</a>
  </li>
</ul>
<p v-else>
  Nothing here yet!
</p>