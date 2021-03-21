<template>
	<li>
		<h2>{{ name }} {{ isFavorite ? '(Favorite)' : '' }}</h2>
		<button @click="toggleFavorite">
			Toggle Favorite
		</button>
		<button @click="toggleDetails">
			{{ detailsAreVisible ? 'Hide' : 'Show' }} Details
		</button>
		<ul v-if="detailsAreVisible">
			<li>
				<strong>Phone:</strong>
				{{ phoneNumber }}
			</li>
			<li>
				<strong>Email:</strong>
				{{ emailAddress }}
			</li>
		</ul>
		<button @click="$emit('delete-contact', id)">Delete Contact</button>
	</li>
</template>

<script>
	export default {
		//props: ['name', 'phoneNumber', 'emailAddress', 'isFavorite'],
		// the below way is useful for working in a team
		props: {
			id: {
				type: String,
				required: true,
			},
			name: { type: String, required: true },
			phoneNumber: { type: String, required: true },
			emailAddress: { type: String, required: true },
			isFavorite: {
				type: Boolean,
				required: false,
				default: false,
				// only true or false, so, no need of a validator here.
				// validator: function(value) {
				// 	return value === '1' || value === '0';
				// },
			},
		},
		// documents component to make it clear to which events it will listen
		emits: ['toggle-favorite', 'delete-contact'],
		// again, this second way is preferable when working in a team, as it describes
		// what does the event need to properly work
		// emits: {
		// 	'toggle-favorite': function(id) {
		// 		if (id) return true;
		// 		else {
		// 			console.warn('Id is missing!');
		// 			return false;
		// 		}
		// 	},
		// },
		data() {
			return {
				detailsAreVisible: false,
			};
		},
		methods: {
			toggleFavorite() {
				// allows to emit custom events that can be listened at the parent component
				// communication child => parent
				this.$emit('toggle-favorite', this.id);
			},
			toggleDetails() {
				this.detailsAreVisible = !this.detailsAreVisible;
			},
		},
	};
</script>
