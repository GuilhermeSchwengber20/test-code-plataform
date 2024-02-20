<template>
  <div
    class="w-screen flex flex-col h-screen justify-center items-center bg-gradient-to-br from-blue-600 to-neutral-800"
  >
    <div
      class=" bg-slate-900 shadow-[0_3px_10px_rgb(0,0,0,0.2)] rounded-md flex flex-col xl:h-[77vh] xl:w-3/4 lg:w-[90vw] md:w-[90vw]"
    >
      <div class="h-10 border-b p-2">
        <span class="font-mono text-gray-200 ml-2">
          The Code Test Generator
        </span>
      </div>
      <div class="flex p-5 gap-5">
        <div class="w-52">
          <label for="languages" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">
            Select an Language
          </label>
          <select @change="handleSelectLanguage" v-model="languageSelected" id="languages" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
            <option v-for="(lang, index) in languages" :key="index" :value="lang">
             {{ lang }}
            </option>
          </select>
        </div>
        <div class="w-52">
          <label for="test-libs" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">
            Select an Test Lib
          </label>
          <select v-model="testLibSelected" id="test-libs" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
            <option v-for="(lib, index) in testLibs" :key="index" :value="lib">
             {{ lib }}
            </option>
          </select>
        </div>
      </div>
      <div class="p-5 w-full flex gap-20">
        <div class="flex flex-col items-end w-1/2">
          <Codemirror 
            v-model:value="snippetCode"
            :options="cmOptions"
            placeholder="# Input code snippet to generate test"
            border
            height="300"
          />
          <button
            @click="sendCodeToTest"
            type="button"
            class="mt-3 text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800">
            
            <svg v-if="loading" aria-hidden="true" class="w-6 h-6 text-gray-50 animate-spin dark:text-gray-50 fill-blue-600" viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z" fill="currentColor"/>
              <path d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z" fill="currentFill"/>
            </svg>
            <label v-else>Generate Test</label>
          </button>
        </div>
        <div class="w-1/2">

          <Codemirror 
            v-model:value="resultedCode"
            :options="cmOptions"
            placeholder="# Result the test Generate"
            border
            height="300"
          />
        </div>
      </div>
    </div>
    <footer class="h-10 w-full text-center">2024 | Desenvolvidor Por <a>Guilherme Schwengber</a></footer>
  </div>
</template>
<script>
import Codemirror from "codemirror-editor-vue3";

import "codemirror/addon/display/placeholder";
import "codemirror/mode/javascript/javascript.js";
import "codemirror/mode/python/python.js";
import "codemirror/theme/dracula.css";

export default {
  name: "AppVue",
  components: { Codemirror },
  data() {
    return {
      secret_key: import.meta.env.VITE_SECRET_API_KEY,
      baseUrl: import.meta.env.VITE_BASE_URL,
      snippetCode: "",
      cmOptions: {
        mode: "text/javascript",
        theme: "dracula",
      },
      resultedCode: "",
      languages: ["Python", "Javascript", "Node.js"],
      testLibs: ["Cypress", "Jest", "PyTest", "Unittest"],

      testLibSelected: "Jest",
      languageSelected: "Javascript",

      loading: false,
    };
  },
  mounted() {
    console.log()
  },
  methods: {
    handleSelectLanguage() {
      if(this.languageSelected === "Python") {
        this.cmOptions.mode = "text/x-python"
      } else {
        this.cmOptions.mode = "text/javascript"
      }
    },
    sendCodeToTest() {
      try {
        const url = `${this.baseUrl}/chat/completions`;
        const body = {
          model: "gpt-3.5-turbo",
          messages: [
            {
              role: "user",
              content: `Faça um teste em ${this.testLibSelected} e me retorne somente o teste do seguinte trecho de codigo na lingauge ${this.languageSelected} sem mensagens a mais: ${this.snippetCode}`,
            },
          ],
          temperature: 0.6,
          top_p: 1,
          n: 1,
          stream: false,
          max_tokens: 2048,
        };
        const jsonString = JSON.stringify(body);
        this.loading = true;
        fetch(url, {
          headers: {
            Authorization: `Bearer ${this.secret_key}`,
            "Content-Type": "application/json",
          },
          method: "POST",
          body: jsonString,
        })
          .then((res) => {
            if (!res.ok) {
            this.loading = false;
              throw new Error(`HTTP error! Status: ${res.status}`);
            }
            return res.json();
          })
          .then((data) => {
            this.loading = false;
            this.resultedCode = data.choices[0].message.content;
          })
          .catch((err) => {
            this.loading = false;
            console.log(err);
          });
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>
