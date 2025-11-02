# Ex06 BMI Calculator
## Date:

## AIM
To create a BMI calculator using React Router 

## ALGORITHM
### STEP 1 State Initialization
Manage the current page (Home or Calculator) using React Router.

### STEP 2 User Input
Accept weight and height inputs from the user.

### STEP 3 BMI Calculation
Calculate the BMI based on user input.

### STEP 4 Categorization
Classify the BMI result into categories (Underweight, Normal weight, Overweight, Obesity).

### STEP 5 Navigation
Navigate between pages using React Router.

## PROGRAM
## BmiCalculator.jsx
```
import React, { useState } from 'react';
import './BmiCalculator.css';

const BmiCalculator = () => {
  const [weight, setWeight] = useState(70);
  const [height, setHeight] = useState(175);
  const [units, setUnits] = useState('metric');
  const [bmi, setBmi] = useState(null);
  const [category, setCategory] = useState('');

  const calculateBMI = () => {
    if (!height || !weight || height <= 0 || weight <= 0) {
      alert('Please enter valid height and weight.');
      return;
    }

    let bmiValue;
    if (units === 'metric') {
      const heightM = height / 100;
      bmiValue = weight / (heightM * heightM);
    } else {
      bmiValue = (703 * weight) / (height * height);
    }

    const result = bmiValue.toFixed(1);
    setBmi(result);

    if (result < 18.5) setCategory('Underweight');
    else if (result < 25) setCategory('Normal');
    else if (result < 30) setCategory('Overweight');
    else setCategory('Obese');
  };

  const resetForm = () => {
    setWeight(units === 'metric' ? 70 : 154);
    setHeight(units === 'metric' ? 175 : 69);
    setBmi(null);
    setCategory('');
  };

  return (
    <div className="bmi-wrapper">
      <h2 className="bmi-title">BMI Calculator</h2>

      <div className="bmi-unit-toggle">
        <label>
          <input
            type="radio"
            checked={units === 'metric'}
            onChange={() => { setUnits('metric'); resetForm(); }}
          />
          Metric (kg, cm)
        </label>
        <label>
          <input
            type="radio"
            checked={units === 'imperial'}
            onChange={() => { setUnits('imperial'); resetForm(); }}
          />
          Imperial (lb, in)
        </label>
      </div>

      <input
        type="number"
        value={weight}
        onChange={(e) => setWeight(e.target.value)}
        placeholder={`Weight (${units === 'metric' ? 'kg' : 'lb'})`}
        className="bmi-input"
      />
      <input
        type="number"
        value={height}
        onChange={(e) => setHeight(e.target.value)}
        placeholder={`Height (${units === 'metric' ? 'cm' : 'in'})`}
        className="bmi-input"
      />

      <button onClick={calculateBMI} className="bmi-btn-primary">
        Calculate
      </button>
      <button onClick={resetForm} className="bmi-btn-secondary">
        Reset
      </button>

      {bmi && (
        <div className="bmi-result-card">
          <p className="bmi-result">Your BMI: <strong>{bmi}</strong></p>
          <p className={`bmi-category ${category.toLowerCase()}`}>
            Category: {category}
          </p>
        </div>
      )}

      <div className="bmi-guide">
        <h4>BMI Categories</h4>
        <ul>
          <li>Underweight — Below 18.5</li>
          <li>Normal — 18.5 to 24.9</li>
          <li>Overweight — 25 to 29.9</li>
          <li>Obese — 30 and above</li>
        </ul>
      </div>
    </div>
  );
};

export default BmiCalculator;

```

## BmiCalculator.css

```
body {
  font-family: 'Poppins', sans-serif;
  background: linear-gradient(135deg, #ffe4e1, #e0f7fa); /* soft pink to light cyan */
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.bmi-wrapper {
  background: #fff0f5; /* lavender blush */
  padding: 2rem;
  border-radius: 16px;
  box-shadow: 0 8px 20px rgba(200, 180, 200, 0.2);
  width: 90%;
  max-width: 420px;
  text-align: center;
  transition: transform 0.3s ease;
}

.bmi-wrapper:hover {
  transform: translateY(-4px);
}

.bmi-title {
  font-size: 1.8rem;
  color: #4b0082; /* indigo */
  margin-bottom: 1.5rem;
  font-weight: 600;
}

.bmi-unit-toggle {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 1rem;
  font-size: 0.9rem;
  color: #6a1b9a; /* purple */
}

.bmi-unit-toggle input {
  margin-right: 5px;
}

.bmi-input {
  width: 100%;
  padding: 0.75rem;
  margin-bottom: 1rem;
  border: 1px solid #d1c4e9; /* pastel purple border */
  border-radius: 10px;
  font-size: 1rem;
  transition: border-color 0.3s;
}

.bmi-input:focus {
  border-color: #7b1fa2; /* vibrant purple */
  outline: none;
}

.bmi-btn-primary,
.bmi-btn-secondary {
  width: 48%;
  padding: 0.7rem;
  margin: 0.3rem;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s;
}

.bmi-btn-primary {
  background-color: #ff6f61; /* coral */
  color: white;
}

.bmi-btn-primary:hover {
  background-color: #e64a19; /* dark coral */
}

.bmi-btn-secondary {
  background-color: #cd8b1a; /* soft orange */
}

.bmi-btn-secondary:hover {
  background-color: #e59b2b;
}

.bmi-result-card {
  margin-top: 1.5rem;
  background: #fce4ec; /* pink pastel card */
  padding: 1rem;
  border-radius: 10px;
  box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.05);
}

.bmi-result {
  font-size: 1.3rem;
  color: #880e4f; /* deep magenta */
}

.bmi-category {
  font-size: 1rem;
  font-weight: 500;
}

.bmi-category.normal {
  color: #43a047; /* green */
}

.bmi-category.underweight {
  color: #1e88e5; /* blue */
}

.bmi-category.overweight {
  color: #a78a08; /* yellow */
}

.bmi-category.obese {
  color: #e53935; /* red */
}

.bmi-guide {
  margin-top: 1.5rem;
  text-align: left;
}

.bmi-guide h4 {
  font-size: 1.1rem;
  color: #6a1b9a; /* purple */
  margin-bottom: 0.5rem;
}

.bmi-guide ul {
  list-style: none;
  padding: 0;
  font-size: 0.9rem;
}

.bmi-guide li {
  background: #df8b0c; /* soft orange list items */
  margin-bottom: 0.3rem;
  padding: 0.4rem 0.6rem;
  border-radius: 6px;
}

```
## App.jsx

```
import React from 'react';
import BmiCalculator from './BmiCalculator';

function App() {
  return (
    <div>
      <BmiCalculator />
    </div>
  );
}

export default App;


```

## OUTPUT

<img width="951" height="853" alt="Screenshot 2025-10-24 182315" src="https://github.com/user-attachments/assets/13f11e9c-dee9-4274-a72b-27c3fa7bda55" />

<img width="1913" height="962" alt="Screenshot 2025-10-24 182101" src="https://github.com/user-attachments/assets/e69a41e5-bd16-4ff8-9199-d5a736a75d8a" />

## RESULT
The program for creating BMI Calculator using React Router is executed successfully.
