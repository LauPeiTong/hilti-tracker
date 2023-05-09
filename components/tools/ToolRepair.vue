<template lang="pug">
  v-card(class="mx-auto rounded-xl" max-width="350" outlined)
    v-img(src="https://i.pinimg.com/originals/65/37/74/653774e85a6e6d07286b7cc10e760835.png"
      height="270px"
      cover
    )

    v-card-title(class="text-center")
      b Prediction Accuracy
    v-card-subtitle(class="text-center")
      b 96.7%

    v-card-title(class="text-center")
      b Please repair before
    v-card-subtitle(class="text-center")
      b 31/1/2023

    v-card-title(class="text-center")
      b Repair Fee
    v-card-subtitle(class="text-center")
      b Free (within warranty period)

    v-card-actions
      v-space
</template>

<script>
export default {
  name: 'ToolRepair'
}
</script>
