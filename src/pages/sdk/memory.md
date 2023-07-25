---
title: Memory
description: Learn how to use the Memory API.
---

## Creating a new memory

Creating a new memory involves generating a unique memory ID that will be used to store embedded data.

This process is abstracted by the SDK and requires no parameters.

```typescript
import { createMemory } from 'polyfact'
;(async () => {
  const memory = await createMemory()
  console.log(memory) // Outputs: { id: '...' }
})()
```

The resulting memory object contains a unique id that represents the new memory. This id will be used when updating the memory or referencing it in other operations.

## Updating an existing memory

Updating an existing memory involves adding embedded data to a previously created memory.

To do this, you'll need the unique memory ID that was generated when the memory was created.

The `updateMemory` function takes two parameters:

1. The unique memory id.
2. The data to be embedded into the memory.

```typescript
import { updateMemory } from 'polyfact'
;(async () => {
  const result = await updateMemory('<memory-id>', '<input-data>')
  console.log(result) // Outputs: { success: true }
})()
```

The `"<input-data>"` should be replaced with the actual data you want to embed into the memory.

The function returns an object that contains a `success` boolean property indicating whether the operation was successful.

## Getting all memories

The `getAllMemories` function retrieves the ids of all memories that have been created. This can be useful when you want to inspect all of your memories or perform operations on multiple memories.

```typescript
import { getAllMemories } from 'polyfact'
;(async () => {
  const memories = await getAllMemories()
  console.log(memories) // Outputs: { ids: ['...', '...', ...] }
})()
```

This function returns an object with an `ids` property, which is an array containing the ids of all created memories.

## Generate response using memory

The `generate` function uses the AI model to generate a response. You can optionally provide the id of a memory created using `createMemory`. The AI will match the prompt with the embedded data in the memory and include the most relevant embeddings in the context.

```typescript
import { generate } from 'polyfact'
;(async () => {
  const response = await generate('<prompt>', '<memory-id>')
  console.log(response) // Outputs: '...'
})()
```

The `"<prompt>"` should be replaced with the task or question you want to generate a response for. If a `"<memory-id>"` is provided, the AI will consider the embedded data in the specified memory when generating the response.

## Full Example

In this example, we'll demonstrate how to create a new memory, update it with some data, retrieve all memories, and generate a response using a memory.

```typescript
import { createMemory, updateMemory, getAllMemories, generate } from 'polyfact'
;(async () => {
  const memory = await createMemory()
  console.log('Created memory:', memory) // Outputs: { id: '...' }

  const result = await updateMemory(memory.id, '<input-data>')
  console.log('Updated memory:', result) // Outputs: { success: true }

  const memories = await getAllMemories()
  console.log('All memories:', memories) // Outputs: { ids: ['...', '...', ...] }

  const response = await generate('<prompt>', memory.id)
  console.log('Generated response:', response) // Outputs: '...'
})()
```
