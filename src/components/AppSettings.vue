<template>
    <div>
        <h2>App Settings</h2>
        <div class="setting">
            <label for="font-size">Font Size</label>
            <button @click="updateFontSize(fontSize - 1)" class="adjust-button">-</button>
            <span>{{ fontSize }}</span>
            <button @click="updateFontSize(fontSize + 1)" class="adjust-button">+</button>
        </div>
        <div class="setting">
            <label for="theme-color">Theme Color</label>
            <select id="theme-color" @change="updateThemeColor($event.target.value)" :value="themeColor">
                <option value="#f4f4f4">Light</option>
                <option value="#333">Dark</option>
                <option value="#FFD700">Gold</option>
                <option value="#ADD8E6">LightBlue</option>
                <option value="#90EE90">LightGreen</option>
            </select>
        </div>
    </div>
</template>

<script>
export default {
    props: ['fontSize', 'themeColor'],
    methods: {
        updateFontSize(newSize) {
            this.$emit('updateFontSize', newSize);
        },
        updateThemeColor(newColor) {
            this.$emit('updateThemeColor', newColor);
        }
    }
};
</script>

<style scoped>
h2 {
    text-align: center;
    margin-bottom: 20px;
}

.setting {
    margin: 20px 0;
    display: flex;
    justify-content: center;
    align-items: center;
}

.adjust-button {
    padding: 10px;
    background-color: #f1f1f1;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    margin: 0 10px;
}

.adjust-button:hover {
    background-color: #e0e0e0;
}

select {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
    background-color: #f9f9f9;
}
</style>