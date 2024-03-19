<template>
	<div class="max-w-3xl my-20 py-12 mx-auto">
	  <h2 class="font-bold text-lg text-gray-600 mb-4">
		Welcome {{ session.user }}!
	  </h2>
	  <!-- <ul>
		<li v-for="item in action.data" :key="item.name">{{ item.name }} - {{ item.modified}}</li>
	  </ul> -->
	  <div class="flex flex-row items-centre justify-between">
	  <h2 class="text-5xl font-bold text-gray-900">Lists</h2>
	  <button icon-left="plus">New List</button>
	  </div>

	  <div class="mt-2">
		<card title= "General">
			<ul>
				<li class="flex flex-row space-y-2 items-centre justify-between" v-for="item in action.data" :key="item.name">
					<span>{{ item.name }} - {{ item.category}}</span>
					<Button @click="completeAction(action.name)" icon="check"/>
				</li>
			</ul>
		</card>
	  </div>
	</div>
  </template>

  <script setup>
  import { ref } from 'vue'
  import { createListResource, Card } from 'frappe-ui'
  import { session } from '../data/session'

  const action = createListResource ({
	doctype: 'Action',
	fields: ["*"],
	limit: 10
  })

  // Define a reactive variable to store the data
  const actionData = ref([])

  // Function to load data
  const loadData = async () => {
	// Await the data loading
	await action.reload()
	// Update the reactive variable with fetched data
	actionData.value = action.data
  }

  // Call the function to load data
  loadData()

  const completeAction = async (actionName) => {
	try {
	  await action.setValue.submit({
		name: actionName,
		category: 'Teaching'
	  })
	} catch (error) {
	  console.error(error)
	}}
  </script>

