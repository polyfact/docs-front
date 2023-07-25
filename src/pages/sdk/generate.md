---
title: LLM generation
description: Learn how to generate a completion using the Polyfact SDK.
---

Polyfact allows you to generate AI responses with or without structured data. This flexibility in the output format makes it easier to handle the AI responses according to the needs of your application.

## Structured Data

The `generateWithType` function generates a response that matches a certain format or "type". This "type" is defined using the `io-ts` package, which allows you to define the shape of the response you want.

### Using `generateWithType`

1. Import `generateWithType` from polyfact.
2. Import `t` from `io-ts` to define the shape of your response.
3. Create a type with `t.type()`.
4. Pass the prompt and the type to `generateWithType()`.

### Example

```js
import { generateWithType } from 'polyfact'
import * as t from 'io-ts'
;(async () => {
  const result = await generateWithType(
    'Count from 1 to 5',
    t.type({ result: t.array(t.number) })
  )

  console.log(result)
})()
```

In this example, `t.type({ result: t.array(t.number) })` defines the shape of the response we want. We want a JSON object with a key `result` and an array of numbers as its value.

The result will be a structured JSON data:

```bash
{ result: [1, 2, 3, 4, 5] }
```

### Type Descriptions

In order to structure the responses from the PolyFact AI, you can define a custom type using the `io-ts` package included in polyfact. This package provides a `t` object, from which you can access different functions to define your custom types. You can chain these functions with `.description()` method to provide an explanation to the AI about what information should be included in each field.

Below is a hypothetical example of a Book Review type:

```js
import { t } from 'polyfact'

const AuthorType = t.type({
  name: t.string.description('The name of the author of the book.'),
  nationality: t.string.description('The nationality of the author.'),
})

const BookReviewType = t.type({
  title: t.string.description('The title of the book being reviewed.'),
  author: AuthorType,
  review: t.string.description('A brief review of the book.'),
  rating: t.number.description('A rating for the book from 1 to 5.'),
  recommend: t.boolean.description('Would you recommend this book to others?'),
})

const ResponseBookReview = BookReviewType
```

In this example, `BookReviewType` is a custom type that represents a book review. It includes the title of the book, the author's information (which is another custom type `AuthorType`), a brief review of the book, a numerical rating, and a recommendation.

By defining a type with `t.type()`, you specify the shape of the response that you want from the AI. You then pass this type to `generateWithType()` function along with the prompt. The AI will then return a response that fits the format of the defined type.

This feature allows for more structure in the data that you receive from the AI, making it easier to handle and use in your application.

## Unstructured Data

If you do not need structured data, you can use the `generate` function, which will provide the generated response as a plain string. This function only requires the prompt as an argument.

Here's an example:

```js
import { generate } from 'polyfact'
;(async () => {
  const result = await generate('Count from 1 to 5')

  console.log(result)
})()
```

## Token Usage

If you want to keep track of token consumption during the generation process, you can use the `generateWithTokenUsage` function. It generates the AI response and also returns the token consumption in the input and output.

Here's an example:

```js
import { generateWithTokenUsage } from 'polyfact'
;(async () => {
  const { result, tokenUsage } = await generateWithTokenUsage(
    'Count from 1 to 5'
  )

  console.log('Generated text:', result)
  console.log('Token usage:', tokenUsage)
})()
```

In this example, the result will include the generated text and the number of tokens used for the input and output:

```bash
Generated text: 1, 2, 3, 4, 5
Token usage: { input: 4, output: 10 }
```

These functions provide a great deal of flexibility in how you generate and handle AI responses in your project. You can choose the one that best suits your needs.
