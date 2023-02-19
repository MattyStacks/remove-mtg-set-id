<template>
  <div class="container">
    <h1>Remove Short MTG Set ID</h1>
    <p>I built this to just get the card numbers and the names, and pull out the short list id.</p>
    <div class="input-container">
      <label for="input-field" class="input-label">Input List:</label>
      <textarea v-model="inputList" id="input-field" class="input-field" rows="5" placeholder="Enter a list of strings..."></textarea>
    </div>
    <button @click="removeParentheses" class="button">Submit</button>
    <div class="output-container">
      <label for="output-field" class="output-label">Output List:</label>
      <textarea v-model="modifiedList" id="output-field" class="output-field" rows="5" placeholder="Modified list will appear here..." readonly></textarea>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputList: '',
      modifiedList: ''
    }
  },
  methods: {
    removeParentheses() {
      // Split the input list into an array of strings
      const list = this.inputList.split('\n');

      // Remove the parentheses from each string in the list
      const updatedList = list.map((string) => {
        return string.replace(/\s*\(.*?\)/g, '');
      });

      // Join the modified list into a single string
      this.modifiedList = updatedList.join('\n');
    }
  }
}
</script>

<style scoped>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}
.container {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}
.input-container {
  margin-bottom: 20px;
}
.input-label {
  display: block;
  margin-bottom: 5px;
}
.input-field {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  resize: none;
}
.output-container {
  margin-top: 20px;
}
.output-label {
  display: block;
  margin-bottom: 5px;
}
.output-field {
  width: 100%;
  height: 200px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  resize: none;
}
.button {
  display: block;
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
}
.button:hover {
  background-color: #0062cc;
}
/* Styles go here */
</style>
