<template lang="pug">
  form.w-full.max-w-sm
    div.mb-6(class='md:flex md:items-center')
      div(class='md:w-1/3')
        label.block.text-gray-500.font-bold.mb-1.pr-4(class='md:text-right md:mb-0' for='inline-full-name')
          | Full Name
      div(class='md:w-2/3')
        input#inline-full-name.bg-gray-200.appearance-none.border-2.border-gray-200.rounded.w-full.py-2.px-4.text-gray-700.leading-tight(class='focus:outline-none focus:bg-white focus:border-purple-500' type='text' value='Jane Doe')
    div.mb-6(class='md:flex md:items-center')
      div(class='md:w-1/3')
        label.block.text-gray-500.font-bold.mb-1.pr-4(class='md:text-right md:mb-0' for='inline-password')
          | Password
      div(class='md:w-2/3')
        input#inline-password.bg-gray-200.appearance-none.border-2.border-gray-200.rounded.w-full.py-2.px-4.text-gray-700.leading-tight(class='focus:outline-none focus:bg-white focus:border-purple-500' type='password' placeholder='******************')
    div.mb-6(class='md:flex md:items-center')
      div(class='md:w-1/3')
      label.block.text-gray-500.font-bold(class='md:w-2/3')
        input.mr-2.leading-tight(type='checkbox')
        span.text-sm
          | Send me your newsletter!
    div(class='md:flex md:items-center')
      div(class='md:w-1/3')
      div(class='md:w-2/3')
        button.shadow.bg-purple-500.text-white.font-bold.py-2.px-4.rounded(class='hover:bg-purple-400 focus:shadow-outline focus:outline-none' type='button' @click='goLector')
          | Sign Up
</template>

<script>
export default {
  methods: {
    goLector () {
      this.$router.push('/lector')
    }
  }
}
</script>

<style></style>
