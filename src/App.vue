<template>
  <div class="app">
    <h1>Тестовое задание VueJS</h1>
    <div class="top">
      <div class="top-left">
        <h2>Выбранные вещи (до 6)</h2>
        <ul>
          <li v-for="item in selectedLeftItems" :key="item.id">{{ item.name }}</li>
        </ul>
      </div>
      <div class="top-right">
        <h2>Выбранная вещь</h2>
        <div v-if="selectedRightItem">{{ selectedRightItem.name }}</div>
        <div v-else>Выберите вещь справа снизу</div>
      </div>
    </div>
    <div class="bottom">
      <div class="bottom-left">
        <h2>Вещи у пользователя</h2>
        <ul>
          <li v-for="item in leftItems" :key="item.id">
            <label>
              <input
                type="checkbox"
                :value="item"
                @change="selectLeftItem(item)"
                :checked="isItemSelected(item)"
                :disabled="isItemDisabled(item)"
              />
              {{ item.name }}
            </label>
          </li>
        </ul>
      </div>
      <div class="bottom-right">
        <h2>Вещи на выбор</h2>
        <ul>
          <li v-for="item in rightItems" :key="item.id">
            <label>
              <input
                type="radio"
                name="rightItem"
                :value="item"
                @change="selectRightItem(item)"
                :checked="item.id === selectedRightItem?.id"
              />
              {{ item.name }}
            </label>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      leftItems: [
        { id: 1, name: 'Shoes 1' },
        { id: 2, name: 'Shoes 2' },
        { id: 3, name: 'Shoes 3' },
        { id: 4, name: 'Shoes 4' },
        { id: 5, name: 'T-shirt 1' },
        { id: 6, name: 'T-shirt 2' },
        { id: 7, name: 'T-shirt 3' },
        { id: 8, name: 'T-shirt 4' },
      ],
      rightItems: [
        { id: 11, name: 'Jacket 1' },
        { id: 12, name: 'Jacket 2' },
        { id: 13, name: 'Jacket 3' },
        { id: 14, name: 'Jacket 4' },
        { id: 15, name: 'Hoodie 1' },
        { id: 16, name: 'Hoodie 2' },
        { id: 17, name: 'Hoodie 3' },
        { id: 18, name: 'Hoodie 4' },
      ],
      selectedLeftItems: [],
      selectedRightItem: null,
    };
  },
  methods: {
    selectLeftItem(item) {
      if (this.selectedLeftItems.includes(item)) {
        this.selectedLeftItems = this.selectedLeftItems.filter((i) => i.id !== item.id);
      } else if (this.selectedLeftItems.length < 6) {
        this.selectedLeftItems.push(item);
      }
    },
    selectRightItem(item) {
      this.selectedRightItem = item;
    },
    isItemSelected(item) {
      return this.selectedLeftItems.some((i) => i.id === item.id);
    },
    isItemDisabled(item) {
      return !this.selectedLeftItems.includes(item) && this.selectedLeftItems.length >= 6;
    },
  },
};
</script>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: Arial, sans-serif;
}

h1 {
  margin-bottom: 20px;
  font-size: 24px;
}

.top, .bottom {
  display: flex;
  justify-content: space-between;
  width: 80%;
  margin-bottom: 30px;
}

.top-left, .top-right, .bottom-left, .bottom-right {
  width: 45%;
  padding: 20px;
  border: 2px solid #ddd;
  border-radius: 10px;
  background-color: #f9f9f9;
  margin-right: 10px;
}

h2 {
  font-size: 18px;
  margin-bottom: 10px;
}

ul {
  list-style: none;
  padding: 0;
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  
}

li {
  margin-bottom: 8px;
}

input[type="checkbox"],
input[type="radio"] {
  margin-right: 10px;
}

.top-left ul li, 
.top-right ul li {
  font-weight: bold;
}

.bottom-left, 
.bottom-right {
  background-color: #fff;
}

label {
  cursor: pointer;
}

input[type="checkbox"]:disabled + label, 
input[type="radio"]:disabled + label {
  color: #ccc;
  cursor: not-allowed;
}
</style>
