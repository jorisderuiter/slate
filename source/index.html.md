---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='https://app.convertcalculator.co'>Go to ConvertCalculator</a>

search: true
---

# Introduction

Welcome to the ConvertCalculator JS API! Create even more versatile calculators using ConvertCalculator's JavaScript API.

# Getting started

First head over [to the editor](https://app.convertcalculator.co). Make sure you have a premium account ([if not, head over to the billing page](https://app.convertcalculator.co/billing)) and toggle the "Use API" switch in in the settings pane in the calculator editor.

Now make sure you have embedded the calculator on your website. After that, you can create an instance of the ConvertCalculator object. The ID of your calculator is required:

```javascript
window.addEventListener('ccloaded', () => {
  const convertcalculator = cc.getInstance('HfJXPJuj5pDCEpLfr');
});
```
# Calculator

## Methods

### addFormData(name, value)
Adds and extra key value pair to a form submission.

```javascript
convertcalculator.calculator.addFormData('No. of Bananas', 12);
```

## on(event, handler)

The way to communicate with the calculator is through events. The following events can be emitted:

Event | Description
--------- | -----------
**submit** | Triggered when a visitor submits a form
**interaction** | Triggered when a visitor interacts with the calculator

```javascript
convertcalculator.calculator.on('submit', (formData) => {
  console.log(formData);
});

convertcalculator.calculator.on('interaction', (questions, formulas) => {
  console.log(questions, formulas);
});
```

# Questions

## Properties

Parameter | Description
--------- | -----------
`questions` | An array of Question objects


## Methods

### getById(questionId)
Get a question model by it's ID. To find an id, `console.log(convertcalculator.questions)`.

```javascript
const question = convertcalculator.questions.getById('uKFTJWxrjHARvFixE');
```


### add(properties)
Add a new question to the calculator.

```javascript
const newQuestion = convertcalculator.questions.add({
  _id: 'sample_id',
  title: 'How much money is in the bananastand?',
  description: 'You tell me, mr. Manager',
  type: 'custom',
  order: 1,
});
```

# Question

## Properties

Parameter | Description
--------- | -----------
`_id` | String
`title` | String
`description` | String
`order` | Number
`type` | String `(range, radio, places, dates, orderList, separator, switch, text)`
`[type]` | Object of type Properties


## Methods

### getAnswer()
Get the current answer to a question programmatically. Every question has a `label` and a `value`. The `label` is a formatted `value`. Some questions (like the Places and Date question) have an extra `data` object that include some additional values (e.g. `isWeekend` in Date and `fromPlaceId` in Places).

```JavaScript
const answer = question.getAnswer();
const { label, value, data } = answer;
```

### setAnswer(answer)
Set the answer to a question programmatically. This will update any formulas in which the question is included/

### setDescription(description)
Set the description of the question programmatically.

### setTitle(title)
Set the title of the question programmatically.

```javascript
  question.setAnswer({ label: '30', value: 35 });
```

### getElement()
Get the DOM element of the question. If you want to create custom HTML, you need to get the DOM element and do something with it.

```javascript
  const questionEl = question.getElement();
  questionEl.innerHTML = '<input type="month" />';
```


# Formulas

## Properties

Parameter | Description
--------- | -----------
`formulas` | An array of Formula objects

## Methods

### getById(formulaId)
Get a Formula model by it's ID. To find an id, `console.log(convertcalculator.formulas)`.

```javascript
const question = convertcalculator.formulas.getById('uKFTJWxrjHARvFixE');
```


### add(properties)
Add a new formula to the calculator.

```javascript
const newFormula = convertcalculator.questions.add({
  _id: 'new_formula',
  title: 'There is always money in the bananastand',
  order: 1,
  equation: 'QA * QC',
});
```

# Formula

## Properties

Parameter | Description
--------- | -----------
`_id` | String
`title` | String
`description` | String
`order` | Number


## Methods

### setEquation(equation)
Set the equation of a formula programmatically.

### setDescription(description)
Set the description of the formula programmatically.

### setTitle(title)
Set the title of the formula programmatically.

```javascript
  const otherValue = 145;
  question.setEquation(`QA * QB * ${otherValue}`);
```

### getElement()
Get the DOM element of the formula.

```javascript
  const formulaEl = formula.getElement();
  formulaEl.innerHTML = '<h3>Completely remove the formula result and replace it with something else.</h3>';
```
