# Llama 2 Dataset Formats

When creating a dataset for Llama2(or most of GPT based models for that matter), there are typically four different dataset formats in my experience.

While these datasets can have sub types of formats, they generally fit in these 3.

Each of these formats vary in their difficulty and their flexibility.  With the easier formats being less flexible in their abilities

## Pretraining Format

This format is the format used to actually pretrain GPT like models.

Its simply a whole butch of text with a BOS and EOS token to mark the beginning of the text.

Base models are trained with this format of dataset.

Models generated with these datasets are not typically as useful outside of few shot and zero shot learning(with creative prompts)

## Simple Format

The simple format is the easiest one to do that can provide value with finetuning.  

You use this one when you want to use these LLMs to accomplish a few tasks and you have input and output pairs for your dataset.

The model will learn to generate an output given an input.

The following is an example of the format:

This example is from a quotes dataset.  The input would be the type of quote, and the actual quote would be the output.

```
<s>success: The successful cannot be unhappy -- it was a contradiction in terms.</s>
```

See a video on this dataset here

### Simple Format With Tags

You could also use tags to clearly mark the start and end of different parts of your input and output.  

Doing this can allow you to easily train a model to do different tasks and allows easy parsing out the output.

You use models trained with this like functions.

```
<s><|START TASK 1|><|START TASK 1 INPUT|>Task 1 input data is here<|END TASK 1 INPUT|><|START TASK 1 OUTPUT|>The correct output given the task and input data<|END TASK 1 OUTPUT|><|END TASK 1|></s>
```

## Instruct Format

The instruct dataset format takes more work, but is great in allowing you to give instructions to LLM and have it perform those tasks.

These models can be flexible on a variety of tasks, and you can also include your own custom tasks to the dataset to have it both be flexible, but good at your custom tasks.

There are many different types of instruct dataset format.  Here is an example of an instruct dataset with and without context.

The following is an example of the format with context:
```
<s>How do you play Baseball?

Output:
Baseball is a game between two teams involving a baseball, which is a ball that is about 2 inches in diameter, and a bat used to hit the ball. Two teams alternate turns pitching and hitting the ball. The hitting team attempts to score as many runs by advancing through the four bases, prior to their team getting three outs during their turn hitting. The pitching team's objective is to prevent the hitting team from scoring runs. Games traditionally last 9 innings, with each team having the opportunity to both hit and pitch 9 times. The team with the most runs after 9 innings wins the game.</s>
```

Without context:

```
<s>How many syllables are in the word smarter?

Output:
There are two syllables in the word smarter: smart-er.</s>
```

## Chat Format

Chat is hardest to get working well.  This is due to the fact that conversations have a high level of variance.  

Having a large diverse dataset, and then using RLHF is typically key to get good results.

The following is an example of the format with for chat llama2 models:

```
[INST]<<SYS>>
You are a friendly chatbot and gives helpful answers
<</SYS>>

Hello[/INST]Hello, how are you?</s><s>[INST]Good, please tell me what 1+1 is.[/INST]1+1=2. Please let me know if you need anything else!</s>
```

Chat models can be with or without system prompts, but having a well working system prompt can give you more control of how the model works.

Thus, having a large diverse dataset, with a large diverse system prompts can be very hard.