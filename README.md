# Llama 2 Dataset Formats

When creating a dataset for Llama2(or most of GPT based models for that matter), there are typically four different dataset formats in my experience.

While these datasets can have subtypes of formats, they generally fit into one of these 4.

Each of these formats varies in their difficulty and their flexibility.  With the easier formats being less flexible in their abilities

## Pretraining Format

This format is the format used to actually pretrain GPT-like models.

It's simply a whole bunch of text with a BOS and EOS token to mark the beginning of the text.

Base models are trained with this format of dataset.

Models generated with these datasets are not typically as useful outside of few-shot and zero-shot learning(with creative prompts)

## Simple Format

The simple format is the easiest one to do that can provide value with finetuning.  

You use this one when you want to use these LLMs to accomplish a few tasks and you have input and output pairs for your dataset.

The model will learn to generate an output given an input.

The following is an example of the format:

This example is from a quotes dataset.  The input would be the type of quote, and the actual quote would be the output.

```
<s>success: The successful cannot be unhappy -- it was a contradiction in terms.</s>
```

See a video on this dataset [here](https://www.youtube.com/watch?v=07ppAKvOhqk&ab_channel=Brillibits)

### Simple Format With Tags

You could also use tags to clearly mark the start and end of different parts of your input and output.  

Doing this can allow you to easily train a model to do different tasks and allows easy parsing of the output.

You use models trained with this format like functions.

```
<s><|START TASK 1|><|START TASK 1 INPUT|>Task 1 input data is here<|END TASK 1 INPUT|><|START TASK 1 OUTPUT|>The correct output given the task and input data<|END TASK 1 OUTPUT|><|END TASK 1|></s>
```

## Instruct Format

The instruct dataset format takes more work but is great in allowing you to give instructions to LLM and have it perform those tasks.

These models can be flexible on a variety of tasks, and you can also include your own custom tasks to the dataset to have it both be flexible, but good at your custom tasks.

There are many different types of instruct dataset formats.  Here is an example of an instruct dataset with and without context.

The following is an example of the format with context:
```
<s>From the text below, tell me where Mount Balinhard got its name.

Input:
Mount Balinhard is a summit in Alberta, Canada.

Mount Balinhard was named for a title bestowed on the Earl of Southesk.

Output:
Balinhard was a title bestowed on the Earl of Southesk, from which Mount Balinhard gets its name.</s>
```

Without context:

```
<s>How many syllables are in the word smarter?

Output:
There are two syllables in the word smarter: smart-er.</s>
```

## Chat Format

Chat is the hardest to get working well.  This is due to the fact that conversations have a high level of variance.  

Having a large diverse dataset, and then using RLHF is typically key to getting good results.

The following is an example of the format for chat llama2 models:

```
[INST]<<SYS>>
You are a friendly chatbot that gives helpful answers
<</SYS>>

Hello[/INST]Hello, how are you?</s><s>[INST]Good, please tell me what 1+1 is.[/INST]1+1=2. Please let me know if you need anything else!</s>
```

Chat models can be with or without system prompts, but having a well-working system prompt can give you more control of how the model works.

Thus, having a large diverse dataset, with a large diverse system prompts can be very hard.
