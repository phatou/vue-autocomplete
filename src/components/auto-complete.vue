<template>
	 <div class="autocomplete">
		<input 
			type="text"
			v-model="search"
			@input="onChange"
		>
		<ul
			v-show="isOpen"
			class="autocomplete-results"
		>
			<li 
				v-for="person in persons"
				:key="person.id"
				@click="setResult(person)"
				class="autocomplete-result"
			>
				{{ person.name }}
			</li>
		</ul>
	</div>
</template>

<script>
export default {
  props: {
    persons: { type: Array, required: true, default: () => [] }
  },
  data() {
    return {
      search: '',
      results: [],
      isOpen: false
    };
  },
  methods: {
    onChange() {
      this.isOpen = true;
      this.filterResults();
    },
    filterResults() {
      this.results = this.persons.filter(
        item => item.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1
      );
    },
    setResult(person) {
      this.search = person.name;
      this.isOpen = false;
    }
  }
};
</script>

<style>
.autocomplete {
  position: relative;
  width: 130px;
}

.autocomplete-results {
  padding: 0;
  margin: 0;
  border: 1px solid #eeeeee;
  height: 120px;
  overflow: auto;
}

.autocomplete-result {
  list-style: none;
  text-align: left;
  padding: 4px 2px;
  cursor: pointer;
}

.autocomplete-result:hover {
  background-color: #4aae9b;
  color: white;
}
</style>
