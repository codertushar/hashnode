---
title: "Accordion Component in JS & React"
seoTitle: "accodion in js and react"
datePublished: Thu Aug 22 2024 05:41:40 GMT+0000 (Coordinated Universal Time)
cuid: cm04uut42001a09jnbf4th22k
slug: accordion-component-in-js-react
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/IV4db_thdMA/upload/ef43438ae37fca61d36945b459f7b842.jpeg
tags: accordion

---

Creating an accordion component in JavaScript is a great way to manage content and improve the user interface. Below is a basic implementation of an accordion component using vanilla JavaScript.

### **HTML Structure:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Accordion Component</title>
    <style>
        .accordion {
            width: 100%;
            max-width: 600px;
            margin: 20px auto;
            border: 1px solid #ddd;
            border-radius: 4px;
            overflow: hidden;
        }

        .accordion-item {
            border-bottom: 1px solid #ddd;
        }

        .accordion-header {
            background-color: #f1f1f1;
            cursor: pointer;
            padding: 15px;
            font-size: 18px;
            font-weight: bold;
        }

        .accordion-content {
            display: none;
            padding: 15px;
            background-color: #fff;
            font-size: 16px;
        }

        .accordion-content.show {
            display: block;
        }
    </style>
</head>
<body>
    <div class="accordion">
        <div class="accordion-item">
            <div class="accordion-header">Section 1</div>
            <div class="accordion-content">Content for section 1.</div>
        </div>
        <div class="accordion-item">
            <div class="accordion-header">Section 2</div>
            <div class="accordion-content">Content for section 2.</div>
        </div>
        <div class="accordion-item">
            <div class="accordion-header">Section 3</div>
            <div class="accordion-content">Content for section 3.</div>
        </div>
    </div>

    <script src="accordion.js"></script>
</body>
</html>
```

### **JavaScript Implementation:**

```javascript
// accordion.js
document.addEventListener('DOMContentLoaded', () => {
    const accordionHeaders = document.querySelectorAll('.accordion-header');

    accordionHeaders.forEach(header => {
        header.addEventListener('click', () => {
            const accordionContent = header.nextElementSibling;

            // Toggle the content visibility
            accordionContent.classList.toggle('show');

            // Optionally close other open accordions (for a single-open accordion)
            accordionHeaders.forEach(item => {
                if (item !== header) {
                    item.nextElementSibling.classList.remove('show');
                }
            });
        });
    });
});
```

### **How It Works:**

1. **HTML Structure**:
    
    * The accordion is made up of `accordion-item` divs, each containing a `accordion-header` for the clickable header and a `accordion-content` for the hidden content.
        
2. **CSS Styling**:
    
    * The `.accordion-content` class is initially hidden using `display: none;`.
        
    * The `.show` class is used to display the content when an accordion item is expanded.
        
3. **JavaScript Logic**:
    
    * **Event Listener**: On `DOMContentLoaded`, an event listener is added to each accordion header.
        
    * **Toggle Functionality**: When a header is clicked, the associated content (`accordionContent`) is toggled by adding/removing the `show` class.
        
    * **Single-Open Behavior** (optional): If you want only one section to be open at a time, the script will close any other open sections by removing the `show` class from their content.
        

### **Customization**:

* You can easily extend this example to include animations, icons, or additional functionality depending on your needs.
    
* To allow multiple sections to be open at once, simply remove the logic that closes other sections.
    

### **Usage**:

This basic accordion component can be used in any project where you need to show and hide sections of content interactively.

\=============================================

In React:  
Creating an accordion component in React is straightforward and allows for more flexibility through the use of state and props. Below is an example of how you can implement a simple accordion component in React.

### **Accordion Component in React:**

#### **1\. Create the Accordion Component:**

```javascript
import React, { useState } from 'react';

const Accordion = ({ title, children }) => {
  const [isOpen, setIsOpen] = useState(false);

  const toggleAccordion = () => {
    setIsOpen(!isOpen);
  };

  return (
    <div className="accordion-item">
      <div className="accordion-header" onClick={toggleAccordion}>
        {title}
        <span>{isOpen ? '-' : '+'}</span>
      </div>
      {isOpen && <div className="accordion-content">{children}</div>}
    </div>
  );
};

export default Accordion;
```

#### **2\. Use the Accordion Component:**

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import Accordion from './Accordion';

const App = () => {
  return (
    <div className="accordion">
      <Accordion title="Section 1">
        Content for section 1.
      </Accordion>
      <Accordion title="Section 2">
        Content for section 2.
      </Accordion>
      <Accordion title="Section 3">
        Content for section 3.
      </Accordion>
    </div>
  );
};

ReactDOM.render(<App />, document.getElementById('root'));
```

#### **3\. Add Basic Styling:**

```css
/* styles.css */
.accordion {
  width: 100%;
  max-width: 600px;
  margin: 20px auto;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.accordion-item {
  border-bottom: 1px solid #ddd;
}

.accordion-header {
  background-color: #f1f1f1;
  cursor: pointer;
  padding: 15px;
  font-size: 18px;
  font-weight: bold;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.accordion-content {
  padding: 15px;
  background-color: #fff;
  font-size: 16px;
}
```

#### **4\. Bring It All Together:**

You can import the CSS file in your React component and then render the `App` component:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import './styles.css';

ReactDOM.render(<App />, document.getElementById('root'));
```

### **How It Works:**

1. **State Management**:
    
    * The `Accordion` component maintains its own open/close state (`isOpen`) using the `useState` hook.
        
2. **Toggle Functionality**:
    
    * The `toggleAccordion` function toggles the `isOpen` state between `true` and `false` when the header is clicked.
        
3. **Conditional Rendering**:
    
    * The content inside the accordion is conditionally rendered based on the value of `isOpen`. When `isOpen` is `true`, the content is displayed; otherwise, it is hidden.
        
4. **Reusability**:
    
    * The `Accordion` component is reusable, allowing you to easily create multiple accordion sections by simply passing different titles and content as props.
        
        ### **Features and Flexibility:**
        
        1. **Reusability**:
            
            * Each instance of the `Accordion` component can be customized with different content, making it easy to reuse across various parts of your application.
                
        2. **Icons or Indicators**:
            
            * You can add indicators like `+` and `-` to show the open/close state, as done in the example with `{isOpen ? '-' : '+'}`. This can be customized further with icons or other visual elements.
                
        3. **Single Open Section (Optional)**:
            
            * If you want to limit the accordion so that only one section can be open at a time, you can manage the open state at a higher level, such as in the `App` component, and pass it down to each `Accordion` component as props.
                
        4. **Styling and Animation**:
            
            * You can easily add CSS transitions to animate the opening and closing of the accordion content, providing a smoother user experience.
                
        5. **Accessibility**:
            
            * To improve accessibility, you can add ARIA attributes like `aria-expanded` and `role` to the headers and content to make it easier for screen readers to navigate.
                
        
        ### **Enhancing the Component:**
        
        1. **Single Open Accordion**:
            
            * To have only one accordion section open at a time, lift the state up to the parent component (`App`). You can maintain an `activeIndex` state and control which accordion section is open based on this index.
                
        2. **CSS Animations**:
            
            * Add CSS transitions to the `.accordion-content` class for a smooth opening and closing effect. This can be done using the `transition` property in CSS.
                
            
            ```css
            .accordion-content {
              max-height: 0;
              overflow: hidden;
              transition: max-height 0.3s ease;
            }
            
            .accordion-content.show {
              max-height: 200px; /* Or any value based on your content */
            }
            ```
            
        3. **Dynamic Content Loading**:
            
            * If your accordion content needs to be fetched from an API, you can handle this by using the `useEffect` hook inside the `Accordion` component. This allows for dynamic loading and rendering of content as the accordion expands.
                
        
        ### **Example of a Single Open Accordion:**
        
        Here’s how you can modify the `App` component to allow only one section to be open at a time:
        
        ```javascript
        import React, { useState } from 'react';
        import Accordion from './Accordion';
        
        const App = () => {
          const [activeIndex, setActiveIndex] = useState(null);
        
          const toggleAccordion = (index) => {
            setActiveIndex(activeIndex === index ? null : index);
          };
        
          return (
            <div className="accordion">
              {[1, 2, 3].map((num, index) => (
                <Accordion
                  key={index}
                  title={`Section ${num}`}
                  isOpen={activeIndex === index}
                  onToggle={() => toggleAccordion(index)}
                >
                  Content for section {num}.
                </Accordion>
              ))}
            </div>
          );
        };
        
        export default App;
        ```
        
        Then, adjust the `Accordion` component to accept `isOpen` and `onToggle` props:
        
        ```javascript
        const Accordion = ({ title, children, isOpen, onToggle }) => {
          return (
            <div className="accordion-item">
              <div className="accordion-header" onClick={onToggle}>
                {title}
                <span>{isOpen ? '-' : '+'}</span>
              </div>
              {isOpen && <div className="accordion-content">{children}</div>}
            </div>
          );
        };
        ```
        
        ### **Conclusion:**
        
        This React accordion component is a simple yet powerful way to manage collapsible sections of content. It's flexible, reusable, and can be easily extended with additional features like animations, single open behavior, or dynamic content loading. You can tailor it to fit your specific use cases and integrate it into your projects to improve the user experience.