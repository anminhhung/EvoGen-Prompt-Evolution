# EvoGen-Prompt-Evolution
![Evolved Prompt Output](/Media/banner.png "Evolved Prompt Output")
## Description & Method
EvoGen is an evolutionary algorithm that optimizes prompts for text-to-image models for aesthetics, as assessed by @rivershavewings aesthetics model.

### Notebook:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/MagnusPetersen/EvoGen-Prompt-Evolution/blob/main/Notebook/EvoGen.ipynb)

The algorithm is composed of three different AI models, stable diffusion as the generative model, using the [deforum](https://discord.gg/upmXXsrwZc) and the [Stable Diffusion with Jax](https://huggingface.co/blog/stable_diffusion_jax) code, which generates images from prompts, @rivershavewings aesthetics model that rates the resulting images and the evolutionary algorithm that created the prompts at random and then optimizes the prompts based on the rating by using the highest rated prompts to generate the next generation of prompts.

![Model Schema](/Media/model_schema.png "[Model Schema]")
## Usage
### Setup
To run this notebook or any Stable Diffusion notebook you need to accept the [terms of conditions](https://huggingface.co/runwayml/stable-diffusion-v1-5) of RunwayML Stable Diffusion 1.5 on Huggingface.
### Hyperparameters
#### Evolutionary Algorithm Settings

General population settings, such as how many generations the algorithm runs for, how many prompts there are in each generation, and the word length range of the prompts.

* **generations:** How many generations the algorithm runs for.

* **population_count:** How many prompts there are in each generation/how large each generation is.

* **prompt_length_max:** Maximum prompt length when the population is initialized, during evolution this limit can be surpassed.

* **prompt_length_min:** Minimum prompt length when the population is initialized, during evolution this limit can be surpassed.

* **artist_prop:** Probability to sample from the artist list when adding or mutating a word.

* **genre_prop:** Probability to sample from the genre list when adding or mutating a word.

* **custom_prop:** Probability to sample from the custom user-defined list when adding or mutating a word.

The difference between the sum of the three custom lists and 1 is the probability to sample from the English dictionary word list.

* **require_custom_words:** If it is set to "True" the custom list will not just serve as a list to sample from but it will be required that each prompt in the population has min_custom_words words from the list in it. 

* **min_custom_words:** The number of words from the custom list required to be in the prompt.

* **use_aes_words:** Replaces the English dictionary that is the basis of the prompt generation with a curated word list derived from prompts with aethetics ratings 5 or higher from the simulacra aesthetics dataset. The base aesthetics score will be higher but I find the generations to be less interesting.

* **use_aes_engrams:** Replaces the English dictionary that is the basis of the prompt generation with a curated 2- and 3. gram list derived from prompts with aethetics ratings 5 or higher from the simulacra aesthetics dataset. If use_aes_words and use_aes_engrams are ticked both lists are concatinated.

* **delete_prop:** probability to delete a word per word in each prompt after each generation.

* **add_prop:** probability to add a new word per word in each prompt after each generation from the word lists.

* **mutate_prop:** probability to swap out a word per word in each prompt after each generation for a new word from the word lists.

* **shuffle_prop:** The probability to shuffle the order of words per prompt.

* **cross_prop:** The cross-over probability is the probability of the parents of the next generation swapping prompt parts per parent pair.

* **k:** K denotes the rounds in the tournament selection process. A higher K value means fewer parents generate the next generation, this means a higher score increase but less diversity in the prompts.

* **cutoff:** Cutoff aesthetics score to save and display the image and prompt.

* **use_prompt:** True if you want to guide the evolution with an additional prompt and not just aesthetics.

* **use_image:** True if you want to guide the evolution with an additional image prompt and not just aesthetics.

* **prompt_weigth:** The weight of prompt & image prompt. For instance 0.6 means the score is the result of 60% prompt+image prompt and 40% aesthetics.

#### Image Generation Settings
Image generation settings have an impact on the speed and behavior of the evolutionary algorithm, the euler_a sampler in conjunction with low step size and resolution is advisable for quick prompt evolution. Good prompts can then later be used to generate higher-quality images.

* **num_inference_steps:** The number of denoising steps. A higher step number will increase image quality but take longer to generate.

## Acknowledgement 
[Stable Diffusion](https://github.com/CompVis/stable-diffusion) by Robin Rombach, Andreas Blattmann, Dominik Lorenz, Patrick Esser, Björn Ommer and the [Stability.ai](https://stability.ai/) Team. [K Diffusion](https://github.com/crowsonkb/k-diffusion) by [Katherine Crowson](https://twitter.com/RiversHaveWings).

The aesthetics model that is an integral part of this method was made by [Katherine Crowson](https://twitter.com/RiversHaveWings) and can be found on her [Github account](https://github.com/crowsonkb/simulacra-aesthetic-models). 

The baseline of the notebook, setup, description, and image generation, is based on the
[deforum](https://discord.gg/upmXXsrwZc) and the [Stable Diffusion with Jax](https://huggingface.co/blog/stable_diffusion_jax) code.
## Examples
### 1. trireme Fantasy Art nondefiling rhinopharyngitis canaliculization cricotracheotomy conure atheology beret Aestheticism Vicente Juan Masip Ashley Bickerton aplustria pelodytoid
<p float="middle">
  <img src="/Media/1.png" width="204" />
  <img src="/Media/2.png" width="204" /> 
  <img src="/Media/3.png" width="204" />
  <img src="/Media/4.png" width="204" />
</p>

### 2. rimal disputants nugget Antoine Blanchard chemosynthesis mentocondylial calculatory supertragical Magic Realism
<p float="middle">
  <img src="/Media/5.png" width="204" />
  <img src="/Media/6.png" width="204" /> 
  <img src="/Media/7.png" width="204" />
  <img src="/Media/8.png" width="204" />
</p>

### 3. harmonics omegoid Peter Blake Vladimir Tretchikoff
<p float="middle">
  <img src="/Media/9.png" width="204" />
  <img src="/Media/10.png" width="204" /> 
  <img src="/Media/11.png" width="204" />
  <img src="/Media/12.png" width="204" />
</p>

## To Do
* **Hyperparameter Tuning:** The hyperparameters are barely tuned and there is a lot of performance to be had when it comes to aesthetics optimization, prompt diversity, and optimization speed. 

* **Evolutionary Algorithm Tuning:** The algorithm is very basic and I have not read much on evolutionary algorithms. Here there is still a lot of room for improvement. Especially the crossover stage of the algorithm might be suboptimal the way it is done now for text.

* **General Features:** There are some features I would like to add, especially having a "base" prompt that is in each population member so that you can take your favorite prompt and build on it.