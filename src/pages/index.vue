<template>
  <VRow class="match-height">
    <VCol
      cols="12"
      sm="6"
      md="4"
      lg="6"
    >
      <VCard>
        <VCardText>
          <VAvatar
            color="error"
            variant="tonal"
            rounded
            size="44"
          >
            <VIcon
              icon="tabler-credit-card"
              size="28"
            />
          </VAvatar>

          <h5 class="text-h5 mt-3">
            Total de Ventes
          </h5>
          <!-- <p class="my-1">
            {{ demo.subTitle }}
          </p> -->
          <p class="mb-3 text-high-emphasis">
            25
          </p>
          <!-- <VChip
            color="error"
            label
            size="small"
          >
            {{ demo.change }}
          </VChip> -->
        </VCardText>
      </VCard>
    </VCol>
    <VCol
      cols="12"
      sm="6"
      md="4"
      lg="6"
    >
      <VCard>
        <VCardText>
          <VAvatar
            color="success"
            variant="tonal"
            rounded
            size="44"
          >
            <VIcon
              icon="tabler-burger"
              size="28"
            />
          </VAvatar>

          <h5 class="text-h5 mt-3">
            Plats servis
          </h5>
          <!-- <p class="my-1">
            {{ demo.subTitle }}
          </p> -->
          <p class="mb-3 text-high-emphasis">
            10000
          </p>
          <!-- <VChip
            color="error"
            label
            size="small"
          >
            {{ demo.change }}
          </VChip> -->
        </VCardText>
      </VCard>
    </VCol>
  </VRow>
</template>
