<template>
  <div class="bg-white p-3 rounded mb-3">
    <div
      class="mt-[10px] w-full font-roboto font-bold font-[18px] leading-[21px] text-[#424242] overflow-hidden text-ellipsis whitespace-nowrap"
    >
      {{ title }}
    </div>
    <div class="flex font-['Roboto'] text-[#7E7E80] dark:bg-gray-700 dark:text-gray-100 rounded-lg text-[13px] font-medium">
      Автор:
      <div class="flex items-center">
        <img
          v-if="creatorFoto"
          :src="creatorFoto"
          class="h-[20px] w-[20px] rounded mx-2"
        >
        <span class="text-[12px]">
          {{ creatorName }}
        </span>
      </div>
    </div>
    <div
      v-if="contributors.length"
      class="mt-[30px] mb-[8px] font-roboto text-[16px] leading-[19px] font-medium text-[#4c4c4d]"
    >
      Сотрудники, прошедшие регламент:
    </div>
    <ReglamentPropsUser
      v-for="contributor in contributors"
      :key="contributor.uid_user"
      :user-uid="contributor.uid_user"
    />
  </div>
</template>

<script>
import ReglamentPropsUser from '@/components/Reglaments/ReglamentPropsUser'

export default {
  components: {
    ReglamentPropsUser
  },
  props: {
    title: {
      type: String,
      default: ''
    },
    creator: {
      type: String,
      default: ''
    },
    contributors: {
      type: Array,
      default: () => ([])
    }
  },
  computed: {
    creatorName () {
      return this.$store.state.employees.employeesByEmail[this.creator]?.name || this.creator
    },
    creatorFoto () {
      return this.$store.state.employees.employeesByEmail[this.creator]?.fotolink
    }
  }
}
</script>

<style scoped>
</style>
