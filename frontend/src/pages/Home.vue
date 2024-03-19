<template>
  <div class="max-w-3xl py-12 mx-auto">
    <h2 class="font-bold text-lg text-gray-600 mb-4">
      Welcome {{ session.user }}!
    </h2>
	<ul>
		Hello!
		{{action.data}}
	</ul>

  </div>
</template>

<script setup>
import { createListResource } from 'frappe-ui'
import { session } from '../data/session'

const action = createListResource ({
	doctype: 'Category description',
	fields: ["*"],
	limit: 10

})
action.reload

</script>
