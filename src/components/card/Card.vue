<script lang="ts">
import { defineComponent, computed } from 'vue'

export default defineComponent({
  name: 'CardComponent',
  components: {},
  setup(props) {
    const isProfessionalCard = computed(() => props.type === 'Professional')
    return { isProfessionalCard }
  },
  props: {
    type: { type: String, required: true },
    monthly: { type: String },
    yearly: { type: String },
    characteristics: { type: Array<string>, required: true },
    action: { type: String, required: true },
    priceType: { type: String, required: true }
  }
})
</script>

<template>
  <div :class="[{ 'purple-card': isProfessionalCard }, 'card']">
    <p class="type-plan">{{ $props.type }}</p>
    <h3 class="price" v-if="$props.priceType === 'monthly'"><span>$</span>{{ $props.monthly }}</h3>
    <h3 class="price" v-else><span>$</span>{{ $props.yearly }}</h3>
    <ul>
      <li v-for="char in characteristics" :key="char" class="characteristics">
        {{ char }}
      </li>
    </ul>
    <button class="cta">{{ $props.action }}</button>
  </div>
</template>

<style scoped>
.card {
  width: 100%;
  background-color: white;
  border-radius: 8px;
  padding: 24px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: #464962;
  margin-bottom: 24px;
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
  max-height: 380px;
  min-width: 215px;

  .type-plan {
    color: #6d708d;
    font-size: 16px;
    margin-bottom: 16px;
  }

  .price {
    font-size: 42px;
    margin-bottom: 24px;
    color: #494c5f;
    display: flex;
    align-items: center;
  }
}

@media (min-width: 768px) {
  .card {
    margin: 0;
   flex-grow: 1;
  }
}

span {
  font-size: 24px;
  margin-right: 4px;
}

ul {
  list-style-type: none;
  padding: 0;
  width: 100%;
  text-align: center;
}

.characteristics {
  font-size: 12px;
  color: #6d708d;
  border-top: 1px solid #b3b5c6;
  padding: 12px;
  width: 100%;
}

.characteristics:last-child {
  border-bottom: 1px solid #b3b5c6;
}

.cta {
  font-family: 'Montserrat', sans-serif;
  margin-top: 24px;
  background: linear-gradient(90deg, #a3a8f0 0%, #6b6fe0 48%);
  border: none;
  padding: 12px 0;
  border-radius: 8px;
  color: white;
  width: 100%;
  cursor: pointer;
}

.cta:hover {
  background: white;
  color: #6e72df;
  border: 1px solid #6b6fe0;
}

.purple-card {
  background: linear-gradient(125deg, rgba(163, 168, 240, 1) 0%, rgba(105, 111, 221, 1) 100%);
  border: none;
  color: white;
  max-height: 450px;
  height: 450px;


  .type-plan {
    color: white;
  }

  .price {
    color: white;
  }
  .characteristics {
    color: white;
  }

  .cta {
    background: white;
    color: #6e72df;
    cursor: pointer;
  }

  .cta:hover {
    background: transparent;
    color: white;
    border: 1px solid white;
  }
}

@media (min-width: 768px) {
  .purple-card {
   flex-grow: 2;
  }
}
</style>
