# Custom Switcher Filter for JetSmartFilters

This repository provides a solution to transform JetSmartFilters radio filters into a visually appealing switcher. Using simple CSS and JavaScript, you can easily apply this functionality to your WordPress site without modifying core plugins.

---

## Features
- Adds a custom switcher style to radio filters.
- Works selectively by applying a specific class (`switcher-filter-style`).
- Fully compatible with JetSmartFilters plugin.
- Simple and easy-to-implement solution.

---

## Requirements
- WordPress with JetSmartFilters plugin installed.
- Basic knowledge of CSS and JavaScript.

---

## Youtube Video

[https://youtube.com/@boostmycroco
](https://youtu.be/V7K-jQAASc0)

## How to Use
1. **Add the `switcher-filter-style` class** to the desired JetSmartFilters widget in Elementor or any editor you're using.
2. **Copy and paste the CSS** into your theme's stylesheet or a custom CSS plugin:
   ```css
   .switcher-filter-style .jet-radio-list__input {
       opacity: 0;
       position: absolute;
       width: 0;
       height: 0;
   }

   .switcher-filter-style .jet-radio-list__label {
       display: none;
   }

   .switcher-filter-style .jet-radio-list__button {
       width: 60px;
       height: 30px;
       background-color: #ccc;
       border-radius: 15px;
       border: 2px solid #ccc;
       position: relative;
       transition: background-color 0.3s ease-in-out, border-color 0.3s ease-in-out;
       cursor: pointer;
   }

   .switcher-filter-style .jet-radio-list__button::after {
       content: "OFF";
       width: 26px;
       height: 26px;
       background-color: white;
       border-radius: 50%;
       position: absolute;
       top: 2px;
       left: 2px;
       color: #000;
       display: flex;
       align-items: center;
       justify-content: center;
       font-size: 10px;
       font-weight: bold;
       transition: transform 0.3s ease-in-out, background-color 0.3s ease-in-out;
   }

   .switcher-filter-style .jet-radio-list__input:checked ~ .jet-radio-list__button {
       background-color: #4caf50;
       border-color: #4caf50;
   }

   .switcher-filter-style .jet-radio-list__input:checked ~ .jet-radio-list__button::after {
       transform: translateX(30px);
       background-color: green;
       color: #fff;
       content: "ON";
   }

 3. **Add the JavaScript to your theme's JavaScript file or enqueue it:**
  
  ```javascript
  document.addEventListener('DOMContentLoaded', () => {
    const switcherFilters = document.querySelectorAll('.switcher-filter-style .jet-radio-list__item');

    switcherFilters.forEach(item => {
        const input = item.querySelector('.jet-radio-list__input');
        const button = item.querySelector('.jet-radio-list__button');

        item.addEventListener('click', () => {
            const isChecked = input.checked;

            if (isChecked) {
                input.checked = false;
                input.value = 'false';
            } else {
                input.checked = true;
                input.value = 'true';
            }

            // Dispatch a change event to trigger any listeners
            input.dispatchEvent(new Event('change'));
        });
    });
});




