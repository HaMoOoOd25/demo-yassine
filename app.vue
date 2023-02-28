

<template>
	<div class="flex justify-center">
		<div class="max-x-4xl mt-5">
			<div class="flex gap-2">
				<div
					@click="option = 0"
					class="border-2 rounded-md hover:bg-gray-200 cursor-pointer w-32 h-32 flex justify-center items-center"
					:class="option == 0 ? 'bg-gray-200' : 'bg-white'"
				>
					<span> Multi Select </span>
				</div>
				<div
					@click="option = 1"
					class="border-2 rounded-md hover:bg-gray-200 cursor-pointer w-32 h-32 flex justify-center items-center"
					:class="option == 1 ? 'bg-gray-200' : 'bg-white'"
				>
					<span> Single Select </span>
				</div>
			</div>

			<div class="mt-3">
				<h1>New Option</h1>
				<div>
					<input
						v-model="optionName"
						type="text"
						class="border-2 rounded-sm py-1 px-2"
						placeholder="Name"
					/>
					<input
						type="file"
						accept=".jpeg,.jpg,.png,image/jpeg,image/png"
						aria-label="upload image button"
						@change="selectFile"
					/>
					<button @click="addOption">Add</button>
				</div>
			</div>

			<div class="mt-3">
				<h1>Options</h1>
				<div class="grid grid-cols-3 gap-3">
					<div
						@click="selectedOption = option.id"
						v-for="option in options"
						:key="option.id"
						class="shadow-xl rounded-md w-56 h-56"
						:class="
							selectedOption == option.id
								? 'border-2 border-indigo-600'
								: ''
						"
					>
						<img
							:src="option.image"
							class="h-32 w-full object-cover object-center"
							alt=""
						/>
						<h1>{{ option.name }}</h1>
						<p>{{ option.description }}</p>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			option: "",
			selectedOption: null,
			imageURL: "",
			optionName: "",
			options: [
				{
					id: 1,
					name: "Option 1",
					description: "desc",
					image: "https://www.microprinting.ca/storage/2017/12/business-card-1024x504.jpg",
				},
				{
					id: 2,
					name: "Option 2",
					description: "desc",
					image: "https://media.gettyimages.com/id/1372272108/vector/corporate-business-card.jpg?s=612x612&w=gi&k=20&c=QXy660KnY9tp8TZTOxOkPjvzWuIiLGeSK9JVKfxPKYU=",
				},
				{
					id: 3,
					name: "Option 3",
					description: "desc",
					image: "https://www.shutterstock.com/image-vector/vector-modern-creative-clean-business-260nw-291548753.jpg",
				},
				{
					id: 4,
					name: "Option 4",
					description: "desc",
					image: "https://img.freepik.com/free-vector/elegant-business-card-blue-white-business-card_1435-1537.jpg?w=2000",
				},
			],
		};
	},

	methods: {
		addOption() {
      console.log(this.imageURL)
			this.options.push({
				name: this.optionName,
				image: this.imageURL,
			});
			this.optionName = "";
			this.imageURL = "";
		},
		async selectFile(e) {
			let file = e.target.files[0]
      this.imageURL = URL.createObjectURL(file)
		},
	},
};
</script>
