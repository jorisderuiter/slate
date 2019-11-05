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
window.addEventListener("ccloaded", () => {
  const ccInstance = cc.getInstance("HfJXPJuj5pDCEpLfr");
});
```

# Calculator

## Methods

### addFormData(name, value)

Adds and extra key value pair to a form submission.

```javascript
ccInstance.calculator.addFormData("No. of Bananas", 12);
```

### on(event, handler)

The way to communicate with the calculator is through events. The following events can be emitted:

| Event           | Description                                            |
| --------------- | ------------------------------------------------------ |
| **submit**      | Triggered when a visitor submits a form                |
| **interaction** | Triggered when a visitor interacts with the calculator |

```javascript
ccInstance.calculator.on("submit", formData => {
  console.log(formData);
});

ccInstance.calculator.on("interaction", (questions, formulas) => {
  console.log(questions, formulas);
});
```

# Questions

## Properties

| Parameter   | Description                  |
| ----------- | ---------------------------- |
| `questions` | An array of Question objects |

## Methods

### getByReference(questionReference)

Get a question model by it's Reference (eg. QA).

```javascript
const question = ccInstance.questions.getByReference("QA");
```

# Question

## Properties

| Parameter     | Description                                                                |
| ------------- | -------------------------------------------------------------------------- |
| `_id`         | String                                                                     |
| `reference`   | String                                                                     |
| `title`       | String                                                                     |
| `description` | String                                                                     |
| `order`       | Number                                                                     |
| `type`        | String `(range, radio, places, dates, orderList, separator, switch, text)` |
| `[type]`      | Object of type Properties                                                  |

## Methods

### on(event, handler)

The way to communicate with the qyestuib is through events. The following events can be emitted:

| Event           | Description                                          |
| --------------- | ---------------------------------------------------- |
| **valueChange** | Triggered when a visitor interacts with the question |

```javascript
const QA = ccInstance.questions.getByReference("QA");
QA.on("valueChange", answer => {
  console.log("Answer:", answer);
});
```

### getAnswer()

Get the current answer to a question programmatically. Every question has a `label` and a `value`. The `label` is a formatted `value`. Some questions (like the Places and Date question) have an extra `data` object that include some additional values (e.g. `isWeekend` in Date and `fromPlaceId` in Places).

```JavaScript
const answer = question.getAnswer();
const { label, value, data } = answer;
```

### setAnswer(answer)

Set the answer to a question programmatically. This will update any formulas in which the question is included/

```javascript
question.setAnswer({ label: "30", value: 35 });
```

### getElement()

Get the DOM element of the question. If you want to create custom HTML, you need to get the DOM element and do something with it.

```javascript
const questionEl = question.getElement();
questionEl.innerHTML = '<input type="month" />';
```

# Formulas

## Properties

| Parameter  | Description                 |
| ---------- | --------------------------- |
| `formulas` | An array of Formula objects |

## Methods

### getByReference(formulaReference)

Get a Formula model by it's reference (e.g. FA).

```javascript
const question = ccInstance.formulas.getByReference("FA");
```

# Formula

## Properties

| Parameter     | Description |
| ------------- | ----------- |
| `_id`         | String      |
| `reference`   | String      |
| `title`       | String      |
| `description` | String      |
| `order`       | Number      |

## Methods

### getResult()

Get the current formula result. This is an object that contains `result`, `resultFormatted` and `resultFormattedFull`.

```javascript
const formulaResult = formula.getResult();
console.log(`The number: ${formulaResult.result}`);
console.log(`The formatted number: ${formulaResult.resultFormatted}`);
console.log(
  `The formatted number with prefix and suffix: ${formulaResult.resultFormattedFull}`
);
```

### getElement()

Get the DOM element of the formula.

```javascript
const formulaEl = formula.getElement();
formulaEl.innerHTML =
  "<h3>Completely remove the formula result and replace it with something else.</h3>";
```
