<template>
  <div class="movement">
    <div class="content">
      <h4>{{ movement.title }}</h4>
      <p>{{ movement.description }}</p>
    </div>
    <div class="action">
      <img src="@/assets/trash-icon.svg" alt="Remove icon" @click="remove()" />
      <p :class="{ red: isNegative, green: !isNegative }">
        {{ amountCurrency }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { defineProps, toRefs, computed, defineEmits } from "vue";

const currencyFormatter = new Intl.NumberFormat("es-MX", {
  style: "currency",
  currency: "MXN",
});

const props = defineProps({
  movement: {
    type: Object,
  },
});

const { movement } = toRefs(props);

const amountCurrency = computed(() => {
  return currencyFormatter.format(movement.value.amount);
});
const isNegative = computed(() => movement.value.amount < 0);

const emit = defineEmits(["remove"]);

const remove = () => {
  emit("remove", movement.value.id);
};
</script>

<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  border-radius: 8px;
  box-sizing: border-box;
}

.movement .content {
  width: 100%;
}

.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}

h4,
p {
  margin: 0;
  padding: 0;
}

h4 {
  margin-bottom: 8px;
}

.movement .action img {
  margin-bottom: 16px;
}

.red {
  color: red;
}

.green {
  color: green;
}
</style>
