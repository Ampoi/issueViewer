<template>
  <body class="flex flex-col w-screen h-screen text-main bg-base">
    <header class="flex flex-row items-center py-6 px-8">
      <div class="flex flex-row items-end gap-2">
        <h1 class="text-3xl font-bold font-['Poppins']">Issue Viewer</h1>
        <p class="text-main/40">by Ampoi</p>
      </div>
    </header>
    <main class="grow p-4 overflow-y-auto">
      <div class="max-w-xl p-4 border-main/40 border-[0.5px] mx-auto rounded-md flex flex-col gap-4">
        <h1 class="text-4xl text-accent font-['Poppins']">Issues</h1>
        <div class="w-full flex flex-col">
          <div
            class="w-full flex flex-col text-lg py-4 border-b-[0.5px] border-main/40 last:border-0 first:pt-0 last:pb-0"
            v-for="(issue, key) in issues"
            :key="key"
          >
            <div>
              <p class="text-main/40">#{{ issue.number }}</p>
              <p class="-mt-5 ml-3 overflow-hidden text-ellipsis whitespace-nowrap">{{ issue.title }}</p>
            </div>
            <div class="flex flex-row text-sm gap-4 px-2">
              <a
                :href="issue.html_url"
                title="open in GitHub"
                class="text-main/40 hover:text-main duration-100"
              >
                <i class="bi bi-github"></i>
              </a>
            </div>
          </div>
        </div>
      </div>
    </main>
  </body>
</template>
<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@600&display=swap');
</style>
<script setup lang="ts">
import { ref } from "vue"

const issues = ref<Issue[]>([])

const userName = "Ampoi"
const repositoryName = "Stask"

type Label = {

}

type Milestone = {

}

type Issue = {
  "html_url": `https://github.com/Ampoi/stask/issues/${number}`
  "number": number
  "title": string
  "labels": Label[]
  "state": "open" | "close"
  "milestone": Milestone | null
}
fetch(`https://api.github.com/repos/${userName}/${repositoryName}/issues?state=open`)
  .then(async (res)=>{
    const newIssues: Issue[] = await res.json()
    console.log(newIssues);
    
    issues.value = newIssues
  })
</script>