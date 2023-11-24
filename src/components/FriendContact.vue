<template>
	<li>
		<h2>{{ name }} {{ isFavorite === true ? '(Favorite)' : '' }}{{ isFavorite }}</h2>
		<button @click="toggleFavorite">Toggle Favorite</button>
		<button @click="toggleDetails">{{ detailsAreVisible ? 'Hide' : 'Show' }} Details</button>
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
		<button @click="deleteFriend">Delete</button>
	</li>
</template>

<script>
export default {
	// props:['name','phoneNumber','emailAdress','isFavorite'],
	props: {
		id: {
			type: String,
			required: true,
		},
		name: {
			type: String,
			required: true,
		},
		phoneNumber: {
			type: String,
			required: true,
		},
		emailAddress: {
			type: String,
			required: true,
		},
		isFavorite: {
			type: Boolean,
			required: false,
			default: false,
			// validator:function(value){
			//   return value==='1' || value==='0'
			// }
		},
	},
	emits:['toggle-favorite','delete'],
	// emits: {
	// 	'toggle-favorite': function (id) {
			
	// 	},
	// },
	data() {
		return {
			detailsAreVisible: false,
			friend: {
				id: 'manuel',
				name: 'Manuel Lorenz',
				phone: '0123 45678 90',
				email: 'manuel@localhost.com',
			},
			// friendIsFavorite: this.isFavorite
		}
	},
	methods: {
		toggleDetails() {
			this.detailsAreVisible = !this.detailsAreVisible
		},
		toggleFavorite() {
			this.$emit('toggle-favorite', this.id)
		},
		deleteFriend(){
			this.$emit('delete',this.id)
		}
	},
}
</script>
