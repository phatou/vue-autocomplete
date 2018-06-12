<template>
	 <div class="auto-complete">
		<input 
			type="text"
			v-model="inputText"
			@keydown.tab.prevent="complete(0)"
			@focus="focus(true)" 
			@blur="focus(false)"
		>
		<table v-show="focused">
			<tbody>
				<tr 
					v-for="(person, i) in filteredPersons"
					:key="person.id"
					@mousedown="complete(i)"
				>
					<td>{{ person[field] }}</td>
				</tr>
			</tbody>
		</table>
	</div>
</template>

<script>
export default {
  props: {
    value: { type: String, required: false },
    persons: { type: Array, required: true },
    field: { type: String, required: true }
  },
  data() {
    return {
			inputText: '',
			focused: false
    };
  },
  // when the object is created
  created() {
    this.inputText = this.value || '';
  },
  updated() {
    this.$emit('input', this.inputText);
  },
  computed: {
    filteredPersons() {
      return this.persons.filter(
        person => person[this.field].indexOf(this.inputText) != -1
      );
    }
  },
  methods: {
    complete(i) {
			this.inputText = this.filteredPersons[i][this.field];
    },
    focus(f) {
      this.focused = f;
    }
  }
};
</script>

<style>
#app {
  padding: 25px;
  background: #efefef;
  color: #555;
  font-family: helvetica;
}

.form-group {
  margin-bottom: 10px;
}

input {
  height: 20px;
  border-radius: 3px;
  border: 2px solid #888;
  padding: 5px 10px;
  transition: all 0.5s ease-out 0s;
  width: 200px;
}

input:focus {
  outline: none;
  border-color: #2196f3;
  border-radius: 0px;
}

.auto-complete input.has-error {
  border-color: #f44336;
}

.auto-complete table {
  position: absolute;
  width: 224px;
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.1);
  border-radius: 3px;
  border: 2px solid #888;
  border-top: 0px;
  cursor: pointer;
}

.auto-complete table tr {
  background: white;
}

.auto-complete table tr td {
  padding: 10px;
}

.auto-complete table tr:nth-child(even) {
  background: #eee;
}

.auto-complete table tr:hover {
  background: #2196f3;
  color: white;
}
</style>