<template>
  <div class="container">
    <h1 class="mdc-typography--headline1">Remove MTG Edition From Card List</h1>

    <h2 class="mdc-typography--headline1">Instructions:</h2>
    <p>Paste your list with your editions into the text box. Then it will remove the edition from the output.</p>
    <div class="input-container">
      <label for="input-field" class="mdc-typography--subtitle1">Input List:</label>
      <textarea v-model="inputList" id="input-field" class="mdc-text-field__input" rows="5" placeholder="Enter a list of strings..." spellcheck="false"></textarea>
    </div>
    <button @click="removeParentheses" class="mdc-button mdc-button--raised">
      <span class="mdc-button__label">Submit</span>
    </button>
    <div class="output-container">
      <label for="output-field" class="mdc-typography--subtitle1">Output List:</label>
      <textarea v-model="modifiedList" id="output-field" class="mdc-text-field__input" rows="5" placeholder="Modified list will appear here..." readonly spellcheck="false"></textarea>
      <div class="button-container">
        <button v-if="modifiedList" @click="copyToClipboard" class="mdc-button mdc-button--raised mdc-button--unelevated mdc-theme--primary-bg">
          <span class="mdc-button__label">Copy to Clipboard</span>
        </button>
        <button v-if="modifiedList" @click="exportToFile" class="mdc-button mdc-button--raised mdc-button--unelevated mdc-theme--primary-bg">
          <span class="mdc-button__label">Export to File</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputList: "",
      modifiedList: "",
    };
  },
  methods: {
    removeParentheses() {
      // Split the input list into an array of strings
      const list = this.inputList.split("\n");

      // Remove the parentheses from each string in the list
      const updatedList = list.map((string) => {
        return string.replace(/\s*\(.*?\)/g, "");
      });

      // Join the modified list into a single string
      this.modifiedList = updatedList.join("\n");
    },
    copyToClipboard() {
      const el = document.createElement("textarea");
      el.value = this.modifiedList;
      document.body.appendChild(el);
      el.select();
      document.execCommand("copy");
      document.body.removeChild(el);
    },
    exportToFile() {
      const now = new Date();
      const dateString = now.toISOString().split("T")[0];
      const timeString = now.toTimeString().split(" ")[0].replace(/:/g, "-");
      const filename = `modified_list_${dateString}_${timeString}.txt`;

      const data = new Blob([this.modifiedList], { type: "text/plain" });
      const url = window.URL.createObjectURL(data);
      const link = document.createElement("a");
      link.href = url;
      link.download = filename;
      link.click();
      window.URL.revokeObjectURL(url);
    },
  },
};
</script>
<style>
@import url('https://fonts.googleapis.com/icon?family=Material+Icons');
@import url('https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap');
@import url('https://unpkg.com/@material/typography/mdc-typography.min.css');
@import url('https://unpkg.com/@material/textfield/mdc-text-field.min.css');
@import url('https://unpkg.com/@material/button/mdc-button.min.css');
</style>
<style scoped>
/* Styles go here */
</style>
