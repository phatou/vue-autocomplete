<template>
	 <div class="autocomplete">
		<input 
			type="text"
			v-model="search"
			@input="onChange"
			@keyup.down="onArrowDown"
			@keyup.up="onArrowUp"
			@keyup.enter="onEnter"
		>
		<ul
			v-show="isOpen && results.length > 0"
			class="autocomplete-results"
		>
			<li 
				v-for="(person, i) in results"
				:key="person.id"
				@click="setResult(person)"
				class="autocomplete-result"
				:class="{ 'is-active': i === arrowCounter }"
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
      isOpen: false,
      arrowCounter: 0
    };
  },
  mounted() {
    document.addEventListener('click', this.handleClickOutside);
  },
  destroyed() {
    document.removeEventListener('click', this.handleClickOutside);
  },
  methods: {
    handleClickOutside(evt) {
      if (!this.$el.contains(evt.target)) {
        this.isOpen = false;
        this.arrowCounter = -1;
      }
    },
    onArrowDown() {
      if (this.arrowCounter < this.results.length) {
        this.arrowCounter = this.arrowCounter + 1;
      }
    },
    onArrowUp() {
      if (this.arrowCounter > 0) {
        this.arrowCounter = this.arrowCounter - 1;
      }
    },
    onEnter() {
      if (this.arrowCounter !== -1) {
        this.search = this.results[this.arrowCounter].name;
      }
      this.isOpen = false;
      this.arrowCounter = -1;
    },
    onChange() {
      this.isOpen = true;
      this.filterResults();
      if (this.results.length > 0) {
        this.arrowCounter = 0;
      }
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

.autocomplete-result.is-active,
.autocomplete-result:hover {
  background-color: #4aae9b;
  color: white;
}
</style>
