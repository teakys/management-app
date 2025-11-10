<script setup lang="ts">
import { ProjectsQuery } from '@/utils/supaQueries'
import { columns } from '@/utils/tableColumns/projectsColumns'
import type { Projects } from '@/utils/supaQueries'

usePageStore().pageData.title = 'Projects'

const projects = ref<Projects | null>(null)
const getProjects = async () => {
  const { data, error, status } = await ProjectsQuery

  if (error) useErrorStore().setError({ error, customCode: status })
  projects.value = data
}

await getProjects()
</script>

<template>
  <DataTable v-if="projects" :columns :data="projects" />
</template>
