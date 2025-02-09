<script lang="ts" setup>
import { computed, onMounted, ref } from "vue";
import { VForm } from 'vuetify/components/VForm';

// Liste des ingrédients
const ingredients = ref([]);

// État du formulaire
const selectedIngredientId = ref<number | null>(null);
const quantity = ref<number | null>(null);
const refForm = ref<VForm | null>(null);

// Calculer l'unité de mesure en fonction de l'ingrédient sélectionné
const selectedIngredient = computed(() =>
  ingredients.value.find(i => i.idIngredient === selectedIngredientId.value)
);
const unitMeasure = computed(() => selectedIngredient.value?.idUniteMesure?.nomUnite || "");

// Formater les ingrédients pour affichage dans le select
const formattedIngredients = computed(() =>
  ingredients.value.map(ingredient => ({
    ...ingredient,
    formattedLabel: `${ingredient.nomIngredient} (${ingredient.idUniteMesure.nomUnite})`
  }))
);

const fetchIngredients = async () => {
  try {
    const url = import.meta.env.VITE_API_BASE_URL + "/get_list_ingredient";
    console.log(url)
    const response = await fetch(url);
    if (!response.ok) {
      throw new Error(`Erreur HTTP: ${response.status}`);
    }
    const data = await response.json();
    ingredients.value = data;
  } catch (error) {
    console.error("Erreur lors de la récupération des ingrédients:", error);
  }
};

// Fonction pour soumettre le formulaire
const submitForm = async () => {
  const isValid = await refForm.value?.validate();
  if (!isValid) {
    console.warn("Le formulaire contient des erreurs !");
    return;
  }

  if (!selectedIngredient.value || !quantity.value) {
    console.warn("Veuillez sélectionner un ingrédient et une quantité valide.");
    return;
  }

  const payload = {
    quantite: quantity.value,
    unite: unitMeasure.value
  };

  console.log("Données envoyées :", payload);

  try {
    const response = await fetch("https://api.example.com/ingredients", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(payload)
    });

    if (!response.ok) throw new Error("Erreur lors de l'envoi des données.");

    const result = await response.json();
    console.log("Réponse API :", result);
    alert("Ajout réussi !");
  } catch (error) {
    console.error("Erreur :", error);
    alert("Une erreur s'est produite.");
  }
};

onMounted(fetchIngredients);
</script>

<template>
  <VRow>
    <VCol cols="12" sm="6" md="6">
      <VCard title="Ajouter le stock d'un ingrédient">
        <VForm ref="refForm" @submit.prevent="submitForm">
          <VCol cols="12">
            <VSelect v-model="selectedIngredientId" label="Sélectionner un ingrédient" :items="formattedIngredients"
              item-title="formattedLabel" item-value="idIngredient" required></VSelect>
          </VCol>
          <VCol cols="12">
            <AppTextField v-model="quantity" :label="`Quantité${selectedIngredientId ? ' (' + unitMeasure + ')' : ''}`"
              type="number" min="1" required />
          </VCol>
          <VCol cols="12">
            <VBtn type="submit">
              Ajouter
            </VBtn>
          </VCol>
        </VForm>
      </VCard>
    </VCol>
  </VRow>
</template>
